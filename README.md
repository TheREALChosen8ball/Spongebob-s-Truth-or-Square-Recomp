# SpongeBob's Truth or Square - Windows Recompilation Setup

This package contains the ReXGlue project and build tools. It does not contain the Xbox 360 game image or extracted game files. The setup builds the recompilation from the `DEFAULT.XEX` you provide.

## Requirements

- Windows 10 or 11, 64-bit
- Visual Studio 2022 or later with the Desktop development with C++ workload
- The Clang and LLVM tools component in Visual Studio
- Your own extracted Xbox 360 game dump

The ReXGlue 0.11.0 SDK runtime and CMake package are included. CMake and Ninja come from the Visual Studio installation.

## Extracting an Xbox 360 Disc

If you have an Xbox 360 disc image, [Xbox 360 ISO Extract](https://xbox-360-iso-extract.en.lo4d.com/windows) is a recommended tool for extracting its contents.

## Build

1. Extract this ZIP to a short, writable folder such as `C:\Games\SpongeBobRecomp` to keep compiler paths short.
2. Run `setup.cmd`.
3. When prompted, enter the folder containing your extracted `DEFAULT.XEX` and game files. Setup records that path for code generation and launch; it does not copy your dump. You can instead put the extracted files in the package's `extract` folder before running setup.
4. The script generates the title C++ from your `DEFAULT.XEX` and builds the Release executable.
5. Setup creates `SpongeBob Truth or Square.lnk` in this folder. Use it to launch the game, or run `SpongeBobTruthOrSquare\launch_game.cmd`.

The executable is created at `SpongeBobTruthOrSquare\out\build\win-msvc\Release\SpongeBobTruthOrSquare.exe`. The launcher passes the game data root explicitly.

To choose a different dump later, run setup again and enter its folder. Setup updates the project manifest and `game_data_root.txt` for that location.

## Important Note About Cutscenes

The current runtime stalls while playing Bink movies. The app temporarily hides every `.bik` file under the supplied game root while it runs, so the game skips those cutscenes. It restores the original files on shutdown and recovers temporary names on the next launch after an unexpected exit.

## Contents

- `SpongeBobTruthOrSquare`: title manifest, host application source, and build/launch scripts
- `tools\rexglue-sdk-binary\win-amd64`: ReXGlue SDK 0.11.0 package and runtime files
- `tools\llvm-msvc`: linker used by the Windows build
- `licenses`: ReXGlue and bundled dependency license files

The ZIP excludes the game image, extracted content, generated C++ output, shader caches, and local build products.

## Credits

This project uses [ReXGlue](https://github.com/rexglue/rexglue-sdk), an Xbox 360 recompilation runtime and toolkit. ReXGlue and its bundled dependencies retain their own licenses; see the included `licenses` folder.

## AI Use

ChatGPT Codex assisted with the Windows setup workflow, host-side integration and troubleshooting, documentation, and build configuration. The recompilation is generated from a game dump supplied locally by the user. AI did not provide or generate the game executable, assets, or other copyrighted game data, and no game dump is included in this source package.
