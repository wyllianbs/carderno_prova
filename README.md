# Código LaTeX Para Provas com Gabarito

Código LaTeX personalizável para criação de provas com geração automática de gabarito. Possui layout em múltiplas colunas, destaque de sintaxe para várias linguagens de programação e formatação flexível de questões.

## Características

- **Geração em Modo Duplo**: Alterne entre versões de prova e gabarito.
- **Destaque de Sintaxe**: Suporte integrado para Python, JavaScript, HTML e CSS com tema VSCode Light.
- **Tipos de Questões**: 
  - Questões Verdadeiro/Falso.
  - Múltipla escolha (A-E).
  - Questões baseadas em código.
- **Layout Profissional**: Formato em duas colunas com identidade da universidade.
- **Suporte UTF-8**: Suporte completo para português e caracteres especiais.
- **Marcação Automática de Respostas**: Indicadores visuais para respostas corretas no modo gabarito.

## Início Rápido

### Pré-Requisitos

- Distribuição LaTeX (TeX Live, MiKTeX ou MacTeX).
- Compilador PDFLaTeX.
- Pacotes LaTeX necessários (veja seção de Dependências).

### Uso Básico

1. Clone este repositório:
```bash
git clone https://github.com/wyllianbs/carderno_prova.git
cd carderno_prova
```

2. Configure sua prova em `caderno_prova.tex`:
```latex
\newcommand{\gabarito}{0}       % 0: apenas prova; 1: com gabarito
\newcommand{\numero}{1}         % número da prova
\newcommand{\pt}{1,00}          % pontuação por questão
\newcommand{\pontostotal}{10}   % pontuação total
```

3. Compile:
```bash
pdflatex caderno_prova.tex
```

## Configuração

### Configurações Principais

Edite a seção de configuração em `caderno_prova.tex`:

| Comando | Descrição | Exemplo |
|---------|-----------|---------|
| `\gabarito` | Modo gabarito (0=desligado, 1=ligado) | `{1}` |
| `\numero` | Número da prova | `{1}` |
| `\pt` | Pontos por questão | `{1,00}` |
| `\pontostotal` | Pontuação total da prova | `{10}` |

### Informações da Instituição

Personalize os detalhes da sua instituição:

```latex
\newcommand{\autor}{Prof. Seu Nome}
\newcommand{\professor}{Seu Nome}
\newcommand{\sigla}{UFSC}
\newcommand{\uf}{Universidade Federal de Santa Catarina}
\newcommand{\departamento}{Nome do Departamento}
\newcommand{\disciplina}{Nome da Disciplina}
\newcommand{\codigo}{Código da Disciplina}
```

## Tipos de Questões

### Questões Verdadeiro/Falso

```latex
\item \rtask \ponto{\pt} Texto da sua questão aqui.

{\setlength{\columnsep}{0pt}\renewcommand{\columnseprule}{0pt}
\begin{multicols}{2}
  \begin{answerlist}[label={\texttt{\Alph*}.},leftmargin=*]
    \ifnum\gabarito=1\doneitem[V.]\else\ti[V.]\fi % resposta correta (gabarito)
    \ti[F.]                                       % resposta incorreta
  \end{answerlist}
\end{multicols}
}
```

**Marcação do Gabarito:**
- Gabarito:    `\ifnum\gabarito=1\doneitem[V.]\else\ti[V.]\fi`
- Alternativa: `\ti[F.]`

### Questões de Múltipla Escolha

```latex
\item \rtask \ponto{\pt} Texto da sua questão aqui.

\begin{answerlist}[label={\texttt{\Alph*}.},leftmargin=*]
  \ti Texto da alternativa A.
  \ti Texto da alternativa B.
  
  \di Texto da alternativa C. % resposta correta (gabarito)
  
  \ti Texto da alternativa D.
  \ti Texto da alternativa E.
\end{answerlist}
```

**Marcação do Gabarito:**
- Gabarito:    `\di` (exibe com _checkbox_ quando `\gabarito=1`)
- Alternativa: `\ti`

### Questões com Código

Inclua trechos de código com destaque de sintaxe:

```latex
\item \rtask \ponto{\pt} Analise o código a seguir:

\begin{lstlisting}[style=Python]
def exemplo():
    return "Olá Mundo"
\end{lstlisting}
```

**Linguagens Suportadas:**
- `style=Python`
- `style=JavaScript`
- `style=HTML`
- `style=CSS`

## Código Inline

Use trechos de código inline em questões ou respostas:

```latex
\lstinline[style=JavaScript]|console.log("Hello, World!");|
```

## Exemplos
- [Prova](samples/caderno_prova.pdf)
- [Gabarito](samples/caderno_prova_gabarito.pdf)


## Dependências

Pacotes LaTeX necessários:
- geometry
- fancyhdr
- fontenc, inputenc, babel
- graphicx
- datetime
- multicol, adjmulticol
- listings
- fancyvrb
- mathtools
- hyperref
- hyphenat
- mdframed
- enumitem, cleveref
- zref
- lineno
- cool
- lmodern, amsmath, amsfonts, amssymb, mathptmx
- stackrel
- ragged2e
- lipsum

## Arquivos de Saída

Quando `\gabarito=1`, o PDF é automaticamente renomeado para `*_gabarito.pdf` (versão com gabarito).

## Personalização

### Cores

As cores do tema VSCode Light estão definidas em `definitions.tex`:

```latex
\definecolor{vscodeBackground}{HTML}{FFFFFF}
\definecolor{vscodeForeground}{HTML}{3B3B3B}
\definecolor{vscodeKeyword}{HTML}{0000FF}
\definecolor{vscodeComment}{HTML}{008000}
\definecolor{vscodeString}{HTML}{A31515}
```

Modifique-as para alterar o tema do destaque de sintaxe.

### Layout da Página

Ajuste as margens em `definitions.tex`:

```latex
\geometry{
  hmargin={.8cm,.7cm},
  vmargin={.5cm,.75cm},
  footskip = 2mm,
}
```

### Cabeçalho e Rodapé

Personalize o cabeçalho com o comando `\headerP` e o rodapé na configuração `fancyhdr`.


## Dicas

- Use `\needspace{N\baselineskip}` antes das questões para evitar quebras (coluna ou página) indesejadas.
- O pacote `\lipsum` é usado para texto placeholder nos exemplos.
- Substitua o texto Lorem Ipsum pelas suas questões reais.
- A imagem do logo deve ser colocada no diretório `./figs/`.

## 📜 Licença

Este projeto está licenciado sob a Licença [GNU General Public License v3.0](LICENSE).

## 👤 Autor

**Prof. Wyllian B. da Silva**  
Departamento de Informática e Estatística (INE)  
Universidade Federal de Santa Catarina (UFSC)

---

**Nota**: Este template foi desenvolvido especificamente para uso na UFSC, mas pode ser facilmente adaptado para outras instituições de ensino.
