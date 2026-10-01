# CHIP-8 - Emulador & Assembler

Neste repositório encontra-se a implementação de um emulador em conjunto com um *assembler* criado para a arquitetura CHIP-8. O emulador é responsável por simular o hardware no qual esta linguagem interpretada corria originalmente, enquanto o *assembler* é utilizado para traduzir código escrito numa sintaxe Assembly específica para executáveis compatíveis com a VM do CHIP-8.

---

# Índice

- [O que é o CHIP-8?](#o-que-é-o-chip-8)
  - [Descrição da VM](#descrição-da-vm)
- [Estrutura do Projeto](#estrutura-do-projeto)
- [Emulador (CEMU)](#emulador-cemu)
  - [Funcionalidades](#funcionalidades)
  - [Pré-visualização](#pré-visualização)
  - [Testes](#testes)
- [Assembler (CASM)](#assembler-casm)
  - [ROMs de Exemplo](#roms-de-exemplo)
- [Utilização](#utilização)
  - [Requisitos](#requisitos)
  - [Instalação de Dependências](#instalação-de-dependências)
  - [Clonar o Repositório](#clonar-o-repositório)
  - [Compilação](#compilação)
  - [CEMU](#cemu)
    - [Opções](#opções)
    - [Exemplos de Utilização](#exemplos-de-utilização)
  - [CASM](#casm)
    - [Opções](#opções-1)
    - [Exemplos de Utilização](#exemplos-de-utilização-1)
- [Contribuição](#contribuição)
- [Licença](#licença)

---

# O que é o CHIP-8?

O CHIP-8 é uma linguagem interpretada desenvolvida por Joseph Weisbecker na década de 1970, com o objetivo principal de ser mais simples do que o código de máquina nativo, mantendo-se eficiente em termos de consumo de recursos. A sua simplicidade e eficiência levaram a comunidade a adotá-la, especialmente no contexto do desenvolvimento e recriação de jogos.

## Descrição da VM

- **Memória:** 4KB (4.096 bytes)
- **Registadores:** 
  - 16x registadores de uso geral de 8 bits (V0..V15 ou V0..VF)
  - 1x registador de índice de 12 bits para apontar para endereços de memória
- **Pilha (*Stack*):** utilizada para armazenar o endereço do PC (*Program Counter*) aquando da chamada de uma subrotina, permitindo retomar a execução nesse endereço após o retorno
- **Temporizadores:** 2 temporizadores de 8 bits
  - **Temporizador de Atraso (*Delay Timer - DT*):** utilizado para temporização de eventos no jogo
  - **Temporizador de Som (*Sound Timer - ST*):** utilizado para efeitos sonoros
- **Gráficos:** ecrã monocromático de 64x32 pixéis (2.048 pixéis no total)
- **Som:** emissão de um sinal sonoro (*beep*) quando o valor do registador ST é superior a zero
- **Opcodes:** o CHIP-8 original possui 35 opcodes, todos com 2 bytes de comprimento armazenados em [Big-Endian](https://en.wikipedia.org/wiki/Endianness) na memória

> [!WARNING]
> Neste projeto foram implementadas 34 das 35 instruções originais. A instrução não implementada (`0NNN`, ou `sys`) era utilizada para executar código de máquina fora do interpretador CHIP-8, algo que não é útil neste contexto nem necessário para a esmagadora maioria das ROMs existentes.

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


