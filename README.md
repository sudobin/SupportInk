1. Download and extract it
Download it, extract it, open SupportInk.slnx in Visual Studio, and press Build.

Use the source package from my previous response:

Download SupportInk source

Extract it somewhere simple, for example:

C:\Projects\SupportInk

You should see roughly:

Plain Text
SupportInk
├── SupportInk.slnx
├── README.md
├── LICENSE.txt
├── src
│ └── SupportInk
│ ├── SupportInk.csproj
│ ├── App.xaml
│ ├── OverlayWindow.xaml
│ ├── ToolbarWindow.xaml
│ └── ...
└── tests
2. Install Visual Studio

Install Visual Studio 2026 Community or the edition your company provides.

In Visual Studio Installer, select:

Desktop & Mobile → .NET desktop development

Also make sure the.NET 10 SDK is installed. The project targets .NET 10 LTS. Microsoft currently documents .NET 10 as a supported LTS release.

3. Open the project

Double-click:

SupportInk.slnx

Visual Studio should load the two projects.

Let NuGet package restore finish.

Then use:

Build → Build Solution

If it succeeds, we have our first important milestone.

4. Run it

Press:

F5

or click the green Start ▶ button.

The toolbar should appear.

Try opening Chrome/Edge, PowerPoint or another application underneath it.

Test these first

Red pen
 Draw directly over the live screen.

Yellow highlighter
 Highlight something on the screen.

Eraser
 Remove a stroke.

Undo
 Remove your most recent stroke.

Clear
 Remove everything.

And most importantly:

Ctrl + Shift + D

This toggles between drawing and interacting with the application underneath.

The underlying application should continue running while you're drawing because we're using the overlay approach rather than drawing onto a screenshot. WPF provides the InkCanvas functionality we're using for digital ink.

5. Don't use it with a customer yet

First let's get it running locally and test:

Does the toolbar appear?
Can you draw over Edge?
Does a YouTube video continue playing underneath the drawing?
Does Ctrl+Shift+D let you interact with the page again?
Does the ink remain visible in interact mode?
Does it behave correctly on your second monitor, if you have one?
Can you share the entire screen in Teams and see the annotations from the receiving side?

That last test is particularly important for your Technical Support Engineer use case.

After that, I'll turn it into a proper application

Once the basic engine is verified on your Windows machine, the target should be something like:

SupportInk v1.0

polished floating toolbar
customizable pen colors
pen thickness selector
highlighter
arrow / rectangle / circle
text annotations
eraser
undo / redo
clear screen
keyboard shortcuts
multi-monitor selection
proper pen/tablet support
settings screen
start-with-Windows option
tray icon
crash recovery
signed .exe
signed MSIX installer
enterprise-friendly deployment
no telemetry/customer-data collection
Teams/customer-support testing

Then the experience for you becomes simply:

Install → Start SupportInk → Customer call → press shortcut → draw → press shortcut → continue working.
======================

Alternate ways to Build/Compile :
Best alternatives

1. .NET SDK + Command Prompt/PowerShell, recommended

Install the .NET 10 SDK, extract the source, open PowerShell in the SupportInk folder, then:

PowerShell
dotnet restore
dotnet build SupportInk.slnx -c Release

To produce a standalone Windows build:

PowerShell
dotnet publish src/SupportInk/SupportInk.csproj -c Release -r win-x64 --self-contained true

The output will be under roughly:

Plain Text
src\SupportInk\bin\Release\net10.0-windows\win-x64\publish\

That is the route I'd recommend if you don't want Visual Studio.

2. Visual Studio Code

Install:

Visual Studio Code
.NET 10 SDK
Microsoft's C# Dev Kit extension

Then open the extracted SupportInk folder and build from VS Code's terminal using the same dotnet commands.

3. GitHub Actions / Azure DevOps

For the eventual production version, I'd actually set up a Windows CI pipeline. Every change can automatically:

compile SupportInk,
run tests,
create the x64 release,
package the application,
eventually code-sign it,
produce a downloadable build artifact.

This is a much better long-term approach for something you'll rely on during customer support sessions.
