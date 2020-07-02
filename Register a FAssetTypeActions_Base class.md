# Registering FAssetTypeActions_Base classes
<h3>Included Dependencies (In EditorModule.build.cs)</h3>
Ensure that your editor module includes the following public dependencies.

```cs
PublicDependencyModuleNames.AddRange(new string[] { "UnrealEd", "SlateCore", "Slate" });
```


<h3>Registering with EditorModule (In EditorModuleName.cpp)</h3>
All asset tools must be registered with the "AssetTools" module before they can be used. In the following Example, 'TestAssetActions' should be replaced with the name of the asset which you just created. Files should be unregistered within ShutdownModule(). Remember to include the required files at the top.

```cpp

#include "TestAssetActions.h"
#include "Templates/SharedPointer.h"
#include "IAssetTools.h"

void FExampleEditor::StartupModule()
{
	IAssetTools& AssetTools = FModuleManager::LoadModuleChecked<FAssetToolsModule>("AssetTools").Get();
	const TSharedRef<IAssetTypeActions> Actions = MakeShareable(new FTestAssetActions());
	AssetTools.RegisterAssetTypeActions(Actions);
	UE_LOG(ExampleEditor, Warning, TEXT("ExampleEditor module has been loaded"));
}
```

