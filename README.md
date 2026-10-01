CHIP8 - Emulator & Assembler
In this repository is my implementation of an emulator along with an assembler created for CHIP-8. The emulator is responsible for simulating the hardware on which this interpreted language originally ran, while the assembler can be used to translate code written in a specific Assembly syntax into executables compatible with the CHIP-8 VM.

Table of contents
What is CHIP-8?
VM Description
Emulator (CEMU)
Features
Preview
Tests
Assembler (CASM)
Example ROMs
Usage
Requirements
Dependency instalation
Cloning the repository
Building
CEMU
Options
Usage
CASM
Options
Usage
Contributing
License
What is CHIP-8?
CHIP-8 is an interpreted language that was developed by Joseph Weisbecker in 1970s, with the main goal of being simpler than machine code itself, while still being efficient in terms of resource consumption. Its simplicity combined with efficiency led the community to adopt its use, especially in the context of game development and recreation.

VM Description
Memory: 4KB (4,096 bytes)
Registers:
16x 8-bit GPRs (V0..V15 or V0..VF)
1x 12-bit index register to point at addresses
Stack: used to store the PC (Program Counter) address when a subroutine is called, so the execution resumes at that address after the subroutine returns
Timers: 2 8-bit timers
Delay timer (DT): used for timing in game events
Sound timer (ST): used for sound effects
Graphics: a 64x32 (2,048 pixels) monochromatic screen
Sound: when the ST value is nonzero, a beeping sound is made
Opcodes: original CHIP-8 has 35 opcodes, which are all two bytes long stored in big-endian at memory
Warning

---

In this project, I implemented 34 of the 35 original instructions, given that the unimplemented instruction (0NNN, or sys) was used to execute machine code outside the Chip-8 interpreter, something that would not be useful in this context and is not required for most ROMs.

---

Emulator (CEMU)
Features
Configurable emulator (IPS, window, audio...).
Well optimized, the ROMs I tested ran smoothly.
Reset key (ESC) to restart the the emulator.
Debugger (not implemented yet)

---

# Estrutura do Projeto

```text
.
├── asm/                  # Ficheiros fonte em Assembly para testes e exemplos (.s)
├── assets/
│   ├── preview/          # Capturas de ecrã para pré-visualização das ROMs
│   └── tests/            # Suíte de testes em ROM (corax+, flags, keypad, beep)
├── docs/                 # Documentação técnica (especificação do CASM)
├── include/              # Ficheiros de cabeçalho C/C++ (.h)
├── src/                  # Código-fonte do emulador (CEMU) e do assembler (CASM)
├── .asm-lsp.toml         # Configuração do Language Server Protocol para Assembly
├── Makefile              # Script de automatização da compilação
├── README.md             # Documentação principal do projeto
└── TODO.md               # Roteiro de desenvolvimento e tarefas pendentes


