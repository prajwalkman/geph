### Runtime Type Introspection In Unreal Engine

Parsing by `HeaderParser.cpp` in `UnrealHeaderTool`:

```cpp
...
if (Token.Matches(TEXT("UPROPERTY"), ESearchCase::CaseSensitive))
{
	CompileVariableDeclaration(AllClasses, Struct, EPropertyDeclarationStyle::UPROPERTY);
	...
	CompileVariableDeclaration(AllClasses, TopNode, EPropertyDeclarationStyle::UPROPERTY);
}
...
```

The `FHeaderParser` class also includes similar functions for compiling other declarations such as `UFUNCTION`, `UINTERFACE`, `UDELEGATE`, etc.

