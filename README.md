# Tizzani.MudBlazor.HtmlEditor

A customizable HTML editor component for [MudBlazor](https://mudblazor.com/), powered by [QuillJS](https://quilljs.com/).

![NuGet Version](https://img.shields.io/nuget/v/Tizzani.MudBlazor.HtmlEditor)
![NuGet Downloads](https://img.shields.io/nuget/dt/Tizzani.MudBlazor.HtmlEditor)
![Last Commit](https://img.shields.io/github/last-commit/erinnmclaughlin/MudBlazor.HtmlEditor)
![License](https://img.shields.io/github/license/erinnmclaughlin/MudBlazor.HtmlEditor)

![image](https://raw.githubusercontent.com/erinnmclaughlin/MudBlazor.HtmlEditor/refs/heads/main/assets/light_mode.png)

Works in dark mode, too!

![image](https://raw.githubusercontent.com/erinnmclaughlin/MudBlazor.HtmlEditor/refs/heads/main/assets/dark_mode.png)

## Installation

Download the [latest release](https://www.nuget.org/packages/Tizzani.MudBlazor.HtmlEditor) from NuGet:

```cmd
dotnet add package Tizzani.MudBlazor.HtmlEditor
```

Add references to the required CSS and JS to your main HTML file (e.g. `App.razor`, `index.html`, or `Page.cshtml` depending on your Blazor setup):

```html
<!-- Add to document <head> -->
<link href="_content/Tizzani.MudBlazor.HtmlEditor/MudHtmlEditor.css" rel="stylesheet" />

<!-- Add to document <body> -->
<script src="https://cdn.jsdelivr.net/npm/quill@2.0.2/dist/quill.js"></script>
<script src="_content/Tizzani.MudBlazor.HtmlEditor/quill-blot-formatter.min.js"></script> <!-- optional; for image resize -->
```

Finally, add the following to your `_Imports.razor`:

```razor
@using Tizzani.MudBlazor.HtmlEditor
```

## Configuring Toolbar Options (available since v2.1)
There are several options available for customizing the HTML editor toolbar.

To customize options for a specific editor instance, define a `<MudHtmlToolbarOptions>` inside the `<MudHtmlEditor>`:

```razor
<MudHtmlEditor>
  <MudHtmlToolbarOptions InsertImage="false" /> <!-- This will exclude the "insert image" toolbar option -->
</MudHtmlEditor>
```

For all available options, see [here](./src/Tizzani.MudBlazor.HtmlEditor/MudHtmlToolbarOptions.razor.cs).

### Configuring Default Options
To configure default options for all instances of the HTML editor, you can wrap your razor content with `<CascadingMudHtmlToolbarOptions>`.

#### App.razor or Routes.razor
```razor
<CascadingMudHtmlToolbarOptions InsertImage="false">
  <Router AppAssembly="@typeof(Program).Assembly">
    <!-- etc. -->
  </Router>
</CascadingMudHtmlToolbarOptions>
```

Child components will inherit the default options, unless they override them with their own `<MudHtmlToolbarOptions>` instance.

### Advanced Customization
For more advanced customization, you can define your own toolbar options inside of an individual `<MudHtmlEditor>` component:

```razor
<MudHtmlEditor>
  <span class="ql-formats">
    <button class="ql-bold" type="button"></button>
    <button class="ql-italic" type="button"></button>
    <button class="ql-underline" type="button"></button>
    <button class="ql-strike" type="button"></button>
  </span>
</MudHtmlEditor>
```

See the [QuillJS documentation](https://quilljs.com/docs/modules/toolbar/) for more information on customizing the toolbar.

## Migrating from v1.0 to v2.0
* Remove the `services.AddMudBlazorHtmlEditor();` call from your `Startup.cs` or `Program.cs` file.
* Remove the `<script src="_content/Tizzani.MudBlazor.HtmlEditor/HtmlEditor.js">` tag from the document body. The required JS is now included by default.
