# __Well Known Project Properties, Items and Item Metadata__

There are two types of properties, items and item metadata that are stored in MSBuild project, targets and props files. 

- [Build  Properties, Items and Item  Metadata](#build-properties-items-and-item-metadata)

- [Design-Time Properties, Items and Item Metadata](#design-time-properties-items-and-item-metadata)

## __Build Properties, Items and Item Metadata__
These properties, items and item metadata can be used to influence builds.

### __Build Properties__

#### __PreBuildEvent (string)__
| Language      | Default            |
|---------------| -------------------|
| C#            | empty ('')         |
| Visual Basic  | empty ('')         |

Specifies commands to execute before the build starts.

##### __Example__
``` XML
  <PropertyGroup>
    <PreBuildEvent>call CopyBuildDependencies.cmd</PreBuildEvent>
  </PropertyGroup>
```

#### __PostBuildEvent (string)__
| Language      | Default            |
|---------------| -------------------|
| C#            | empty ('')         |
| Visual Basic  | empty ('')         |

Specifies commands to excecute after the build ends. To control whether these commands are run on failed or update-to-date builds, set the _RunPostBuildEvent_ property.

##### __Example__
``` XML
  <PropertyGroup>
    <PostBuildEvent>call DeployTestEnvironment.cmd</PostBuildEvent>
  </PropertyGroup>
```

#### __RunPostBuildEvent (enum)__

| Language      | Default            |
|---------------| -------------------|
| C#            | OnBuildSuccess     |
| Visual Basic  | OnBuildSuccess     |

Specifies the conditions for the command in _PostBuildEvent_ to run.

| Value           | Description    |
|-----------------| ---------------|
| Always          | Post-build event will run regardless of whether the build succeeds.     |
| OnOutputUpdated | Post-build event will run only when the project output is different than the previous output.|
| OnBuildSuccess  | Post-build event will run if the build succeeds, regardless of whether the project output is up-to-date.|

##### __Example__
``` XML
  <PropertyGroup>
    <RunPostBuildEvent>Always</RunPostBuildEvent>
  </PropertyGroup>
```

## __Design-Time Properties, Items and Item Metadata__
These properties, items and item metadata are used for solely for Visual Studio and design-time purposes, and have no influence on the resulting build.

### __Design-Time Properties__

#### __AppDesignerFolder (string)__

| Language      | Default            |
|---------------| -------------------|
| C#            | Properties         |
| Visual Basic  | My Project         |

Specifies the name of the _Application Designer_ folder, which by default contains source and other files pertinent to the project as a whole, including AssemblyInfo.cs/AssemblyInfo.vb.

##### __Example__
``` XML
<PropertyGroup>
    <AppDesignerFolder>Dave's Properties</AppDesignerFolder>
<PropertyGroup>
```

#### __AppDesignerFolderContentsVisibleOnlyInShowAllFiles (bool)__

| Language      | Default            |
|---------------| -------------------|
| C#            | false              |
| Visual Basic  | true               |

Specifies whether the contents of the _Application Designer_ folder are only visible when Solution Explorer's _Show All Files_ mode is turned on.

| Value                 | Description    |
|-----------------------| ---------------|
| _true_                | The __Application Designer__ folder's contents are only visible when Solution Explorer's _Show All Files__ mode is turned on.|
| _false_ or empty ('') | The __Application Designer__ folder's contents are always visible.|

##### __Example__
``` XML
<PropertyGroup>
    <AppDesignerFolderContentsVisibleOnlyInShowAllFiles>true</AppDesignerFolderContentsVisibleOnlyInShowAllFiles>
<PropertyGroup>
```

#### __DesignTimeBuild (bool)__

Specifies whether the current build is a [design-time build](design-time-builds.md).

| Value                 | Description    |
|-----------------------| ---------------|
| _true_                | The current build is a design-time build.|
| _false_ or empty ('') | The current build is a normal build.|

##### __Example__
``` XML
  <Target Name="AddAdditionalReferences" BeforeTargets="ResolveAssemblyReference">
     <PropertyGroup Condition="'$(DesignTimeBuild)' == 'true'">
         <_AvoidExpensiveCalculation>true</_AvoidExpensiveCalculation>
     </PropertyGroup>

     ...
  </Target>
```

#### __ProjectGuid (GUID) [deprecated]__

| Language      | Default            |
|---------------| -------------------|
| C#            | empty ('')         |
| Visual Basic  | empty ('')         |

Specifies a unique key of a project within a Visual Studio solution. In the new [C# and Visual Basic project system](http://github.com/dotnet/roslyn-project-system), this is now optional.

##### __Example__
``` XML
<PropertyGroup>
    <ProjectGuid>{3B812812-7B6F-4327-948D-DF7CD21EFE4C}</ProjectGuid>
<PropertyGroup>
```
