### Runtime Type Introspection In Unreal Engine

The first step is for the `UnrealHeaderTool` to parse all header files, looking for macros like `UPROPERTY`, `UCLASS`, `UFUNCTION`, etc.

Parsing by `HeaderParser.cpp` in `UnrealHeaderTool`:

```cpp
if (Token.Matches(TEXT("UPROPERTY"), ESearchCase::CaseSensitive))
{
	CompileVariableDeclaration(AllClasses, Struct, EPropertyDeclarationStyle::UPROPERTY);
	CompileVariableDeclaration(AllClasses, TopNode, EPropertyDeclarationStyle::UPROPERTY);
}
```

The `FHeaderParser` class also includes similar functions for compiling other declarations such as `UFUNCTION`, `UINTERFACE`, `UDELEGATE`, etc. The tool generates one mega cpp file called `{project_name}.generated.cpp` in an `Intermediate` folder, which contains all the generated code for all classes and their members.

Each `UCLASS` block is converted to a new `UClass* MyClass`, and each `UPROPERTY` gets a new `UProperty* MyObject` member inside it.


```cpp
UClass* Z_Construct_UClass_ABob()
{
	OuterClass = ABob::StaticClass();
	UObjectForceRegistration(OuterClass);
	UProperty* NewProp_Phase = new(EC_InternalUseOnlyConstructor, OuterClass, TEXT("Phase"), RF_Public|RF_Transient|RF_Native) UFloatProperty(CPP_PROPERTY_BASE(Phase, ABob), 0x0000000000000001);
	MetaData->SetValue(NewProp_Phase, TEXT("Category"), TEXT("Bobbing"));
	MetaData->SetValue(NewProp_Phase, TEXT("ModuleRelativePath"), TEXT("Bob.h"));
}
```

The `UProperty*` constructor call itself seems to be responsible for *registering* the property as a reflected member of the class. The class itself seems to call a global static function `UObjectForceRegistration(OuterClass);` to register itself.

This approach to reflection is limited in that we have to manually register (in this case, by using a custom parser) each class or member that we are interested in, whereas in languages such as C# and Java, the IL Bytecode is examined at runtime to figure out the types, properties,etc of objects. Obviously parsing bytecode at runtime is extremely slow, so UE's solution is better for high performance applications like games. Not to mention, this was the only way they could get Reflection in C++.

Since all the "reflection" is done at compile time and nothing much happens at runtime, the impact on runtime performance is insignificant.
