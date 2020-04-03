# AVISO

Esse fork é uma experiência sobre adicionar atalhos globais para as funcionalidades implementdas pelo projeto original. 

Em cima do projeto Showcase adicionei funcinalidade que torna o botão esquerdo do mouse um modificador que quando combindo com i move para o VD da direita e quando combindo com u move para o VD da esquerda.

Isso é útil pra mim utilizando um Thinkpad Wireless Keuboard (KT-1255) pois minimiza o deslocamento da mão até as teclas de seta. As demais tentativas de fazer o mesmo utilizando Autohotkey falharam gerando travamento das teclas utilizadas como atalho fazendo com que a UI não repondesse corretamenta aos cliques do mouse e disparando atalhos durante a digitação.

## Bibiotecas adicionais (nuget)

* InputSimulatorCore - propagar a tecla digitada caso o modificador não esteja acionado
* NHotkey.Wpf - escutar eventos

## PInvoke

* GetAsyncKeyState - obter o estado do botão direito do mouse.

## Problemas a serem resolvido

* Acentuação da tecla I e U ( contorno utilizando AltGr quando quero acentuar já que na língua Portuguesa o agudo é o mais utilizado )

## VirtualDesktop

VirtualDesktop is C# wrapper for [IVirtualDesktopManager](https://msdn.microsoft.com/en-us/library/windows/desktop/mt186440%28v%3Dvs.85%29.aspx) on Windows 10.


## Features

* Switch, add, and remove a Virtual Desktop.
* Move the window in the same process to any Virtual Desktop.
* Move the window of another process to any Virtual Desktop (Support in version 2.0 or later).


## Installation

Install NuGet package(s).

```powershell
PM> Install-Package VirtualDesktop
```

* [VirtualDesktop](https://www.nuget.org/packages/VirtualDesktop/) - Core classes for VirtualDesktop.
* [VirtualDesktop.WPF](https://www.nuget.org/packages/VirtualDesktop.WPF/) - Provides extension methods for WPF [Window class](https://msdn.microsoft.com/en-us/library/system.windows.window(v=vs.110).aspx).
* [VirtualDesktop.WinForms](https://www.nuget.org/packages/VirtualDesktop.WinForms/) - Provides extension methods for [Form class](https://msdn.microsoft.com/en-us/library/system.windows.forms.form(v=vs.110).aspx).



## How to use

Preparation: 
```xml
<!-- Please create application manifest file and run without debugging. -->
<compatibility xmlns="urn:schemas-microsoft-com:compatibility.v1">
    <application>
	    <!-- Windows 10 -->
	    <supportedOS Id="{8e0f7a12-bfb3-4fe8-b9a5-48fd50a15a9a}" />
    </application>
</compatibility>
```
```csharp
using WindowsDesktop;
```

Get instance of VirtualDesktop: 
```csharp 
// Get all Virtual Desktops
var desktops = VirtualDesktop.GetDesktops();

// Get Virtual Desktop for specific window
var desktop = VirtualDesktop.FromHwnd(hwnd);

// Get the left/right desktop
var left  = desktop.GetLeft();
var right = desktop.GetRight();
```

Manage Virtual Desktops:
```csharp
// Create new
var desktop = VirtualDesktop.Create();

// Remove
desktop.Remove();

// Switch
desktop.Switch();

```

for WPF window
```csharp
// Need to install 'VirtualDesktop.WPF' package

// Check whether a window is on the current desktop.
var isCurrent = window.IsCurrentVirtualDesktop();

// Get Virtual Desktop for WPF window
var desktop = window.GetCurrentDesktop();

// Move window to specific Virtual Desktop
window.MoveToDesktop(desktop);
```

See also:
* [samples/VirtualDesktop.Showcase](samples/VirtualDesktop.Showcase) project  
![ss150904031950kd](https://cloud.githubusercontent.com/assets/1779073/9666915/d57850d8-52b3-11e5-9d61-b13a49656b11.png)


## License

This library is under [the MIT License](https://github.com/Grabacr07/VirtualDesktop/blob/master/LICENSE).
