# Sistema de Gestão das Olimpíadas (SGO)

> Modelagem UML completa de um sistema para coordenar competições, inscrições de atletas, alocação de locais e controle de resultados olímpicos.

![Status](https://img.shields.io/badge/status-modelagem%20completa-007ec6?style=for-the-badge)
![UML](https://img.shields.io/badge/UML-PlantUML-orange?style=for-the-badge)
![Disciplina](https://img.shields.io/badge/disciplina-Projeto%20de%20Software-6a0dad?style=for-the-badge)
![Curso](https://img.shields.io/badge/curso-Engenharia%20de%20Software-2563eb?style=for-the-badge)

---

## Índice

- [Visão Geral](#visão-geral)
- [Regras de Negócio](#regras-de-negócio)
- [Histórias de Usuário](#histórias-de-usuário)
- [Fluxos e Cenários dos Casos de Uso](#fluxos-e-cenários-dos-casos-de-uso)
- [Diagramas](#diagramas)
  - [Diagrama de Caso de Uso](#diagrama-de-caso-de-uso)
  - [Diagrama de Classes](#diagrama-de-classes)
  - [Diagrama de Pacotes](#diagrama-de-pacotes)
  - [Diagrama de Componentes](#diagrama-de-componentes)
  - [Diagrama de Implantação](#diagrama-de-implantação)
- [Arquitetura](#arquitetura)
- [Padrão de Projeto](#padrão-de-projeto)
- [Estrutura do Repositório](#estrutura-do-repositório)
- [Como Visualizar os Diagramas](#como-visualizar-os-diagramas)
- [Autores](#autores)

---

## Visão Geral

O SGO é um sistema projetado para coordenar os diferentes aspectos de uma Olimpíada. Ele permite o gerenciamento de competições, inscrições de atletas, alocação de locais para as provas e controle de resultados, além de gerar relatórios de medalhas por país.

Este repositório contém exclusivamente a **modelagem e diagramação** do sistema, desenvolvida como trabalho da disciplina de Projeto de Software.

---

## Regras de Negócio

**RN1 — Cadastro de competições**  
O sistema deve permitir o cadastro de competições contendo nome da modalidade, data, horário, local e lista de atletas inscritos.

**RN2 — Inscrição de atletas**  
Atletas de diferentes países podem se inscrever em competições específicas. Cada atleta pode participar de várias competições, mas só pode representar um país por modalidade.

**RN3 — Alocação de locais**  
Os locais devem ser alocados de forma a evitar conflitos de horário. Um local só pode abrigar uma competição por vez.

**RN4 — Controle de resultados**  
Após a realização das competições, os resultados devem ser registrados determinando o atleta vencedor e os classificados em segundo e terceiro lugares.

**RN5 — Relatórios de medalhas**  
O sistema deve gerar relatórios de medalhas mostrando o desempenho de cada país com base nas medalhas de ouro, prata e bronze conquistadas.

---

## Histórias de Usuário

**US01 — Cadastrar competição**  
Como Administrador, quero cadastrar uma competição informando modalidade, data, horário e local, para que ela fique disponível para inscrições de atletas.

**US02 — Editar ou excluir competição**  
Como Administrador, quero editar ou excluir uma competição cadastrada, para corrigir informações ou cancelar eventos.

**US03 — Consultar competições**  
Como Administrador ou Atleta, quero consultar as competições disponíveis, para verificar modalidades, datas e locais.

**US04 — Inscrever atleta em competição**  
Como Atleta, quero me inscrever em uma competição informando o país que represento naquela modalidade, para participar oficialmente do evento.

**US05 — Cancelar inscrição**  
Como Atleta, quero cancelar minha inscrição em uma competição, para me retirar de um evento que não poderei participar.

**US06 — Consultar inscrições**  
Como Atleta, quero consultar minhas inscrições ativas, para acompanhar em quais competições estou registrado.

**US07 — Alocar local para competição**  
Como Organizador, quero alocar um local para uma competição, para garantir que o espaço esteja reservado sem conflito de horário.

**US08 — Verificar disponibilidade de local**  
Como Organizador, quero verificar a disponibilidade de um local em determinada data e horário, para evitar sobreposição de eventos.

**US09 — Liberar local**  
Como Organizador, quero liberar um local após o encerramento de uma competição, para que ele possa ser alocado a outros eventos.

**US10 — Registrar resultado de competição**  
Como Juiz, quero registrar o resultado de uma competição informando o primeiro, segundo e terceiro colocados, para que as medalhas sejam atribuídas corretamente.

**US11 — Atualizar quadro de medalhas**  
Como Sistema, quero atualizar automaticamente o quadro de medalhas sempre que um resultado for registrado, para manter o ranking de países em tempo real.

**US12 — Gerar relatório de medalhas**  
Como Comitê Olímpico, quero gerar um relatório de medalhas agrupado por país, para acompanhar o desempenho de cada nação nas competições.

---

## Fluxos e Cenários dos Casos de Uso

### UC01 — Cadastrar Competição

**Ator principal:** Administrador

**Pré-condição:** Administrador autenticado no sistema. Local disponível cadastrado.

**Fluxo principal:**
1. Administrador acessa o módulo de competições.
2. Seleciona a opção "Cadastrar Competição".
3. Preenche modalidade, data, horário e seleciona um local.
4. Sistema valida os dados informados.
5. Sistema verifica se o local está disponível no horário informado.
6. Sistema registra a competição com status `AGENDADA`.
7. Sistema exibe confirmação do cadastro.

**Fluxo alternativo — local indisponível (passo 5):**
- Sistema informa que o local já possui competição no horário selecionado.
- Administrador escolhe outro local ou outro horário e retorna ao passo 3.

**Fluxo alternativo — dados inválidos (passo 4):**
- Sistema destaca os campos com erro e solicita correção.
- Administrador corrige os dados e retorna ao passo 4.

**Pós-condição:** Competição cadastrada com status `AGENDADA` e disponível para inscrições.

---

### UC02 — Editar / Excluir Competição

**Ator principal:** Administrador

**Pré-condição:** Competição cadastrada com status `AGENDADA`.

**Fluxo principal (editar):**
1. Administrador consulta a lista de competições.
2. Seleciona a competição desejada.
3. Altera os dados necessários, como modalidade, data, horário ou local.
4. Sistema valida os dados alterados.
5. Se o local ou horário for alterado, sistema verifica disponibilidade.
6. Sistema salva as alterações e exibe confirmação.

**Fluxo principal (excluir):**
1. Administrador consulta a lista de competições.
2. Seleciona a competição e escolhe a opção excluir.
3. Sistema solicita confirmação da exclusão.
4. Administrador confirma.
5. Sistema remove a competição e cancela todas as inscrições vinculadas.
6. Sistema exibe confirmação da exclusão.

**Fluxo alternativo — competição em andamento ou concluída:**
- Sistema bloqueia a edição ou exclusão e exibe mensagem informando que a operação não é permitida para competições com status `EM_ANDAMENTO` ou `CONCLUIDA`.

**Pós-condição:** Competição atualizada com os novos dados, ou removida do sistema com inscrições canceladas.

---

### UC03 — Consultar Competições

**Ator principal:** Administrador, Atleta

**Pré-condição:** Nenhuma.

**Fluxo principal:**
1. Ator acessa o módulo de competições.
2. Sistema lista todas as competições cadastradas com modalidade, data, horário, local e status.
3. Ator pode aplicar filtros por modalidade, data ou status.
4. Sistema atualiza a listagem conforme os filtros aplicados.
5. Ator seleciona uma competição para visualizar os detalhes completos.

**Fluxo alternativo — nenhuma competição encontrada:**
- Sistema exibe mensagem informando que não há competições cadastradas ou que correspondam aos filtros aplicados.

**Pós-condição:** Lista de competições exibida ao ator com os filtros aplicados.

---

### UC04 — Inscrever Atleta

**Ator principal:** Atleta

**Pré-condição:** Atleta autenticado no sistema. Competição disponível com status `AGENDADA`.

**Fluxo principal:**
1. Atleta consulta as competições disponíveis.
2. Seleciona a competição desejada e acessa os detalhes.
3. Seleciona a opção "Inscrever-se".
4. Informa o país que irá representar naquela modalidade.
5. Sistema valida se o atleta já não está inscrito na mesma modalidade representando outro país.
6. Sistema valida se ainda há vagas disponíveis na competição.
7. Sistema registra a inscrição vinculando atleta, competição e país representado.
8. Sistema exibe confirmação da inscrição.

**Fluxo alternativo — atleta já inscrito na modalidade por outro país (passo 5):**
- Sistema rejeita a inscrição e exibe mensagem informando que o atleta já representa outro país nessa modalidade.

**Fluxo alternativo — competição com vagas esgotadas (passo 6):**
- Sistema informa que não há vagas disponíveis e não realiza a inscrição.

**Fluxo alternativo — competição não está mais agendada (passo 3):**
- Sistema informa que as inscrições para essa competição estão encerradas.

**Pós-condição:** Inscrição registrada vinculando atleta, competição e país representado.

---

### UC05 — Cancelar Inscrição

**Ator principal:** Atleta

**Pré-condição:** Atleta autenticado com inscrição ativa em competição com status `AGENDADA`.

**Fluxo principal:**
1. Atleta consulta suas inscrições ativas.
2. Seleciona a inscrição que deseja cancelar.
3. Seleciona a opção "Cancelar Inscrição".
4. Sistema solicita confirmação do cancelamento.
5. Atleta confirma.
6. Sistema marca a inscrição como cancelada.
7. Sistema remove o atleta da lista de inscritos na competição.
8. Sistema exibe confirmação do cancelamento.

**Fluxo alternativo — competição já iniciada ou concluída (passo 2):**
- Sistema bloqueia o cancelamento e exibe mensagem informando que não é possível cancelar inscrições em competições com status `EM_ANDAMENTO` ou `CONCLUIDA`.

**Fluxo alternativo — atleta desiste da confirmação (passo 5):**
- Sistema cancela a operação e mantém a inscrição ativa.

**Pós-condição:** Inscrição cancelada e vaga liberada na competição.

---

### UC06 — Consultar Inscrições

**Ator principal:** Atleta

**Pré-condição:** Atleta autenticado no sistema.

**Fluxo principal:**
1. Atleta acessa o módulo de inscrições.
2. Sistema lista todas as inscrições do atleta com competição, modalidade, data, local e status da inscrição.
3. Atleta pode filtrar por status, como ativa ou cancelada, ou por data.
4. Sistema atualiza a listagem conforme os filtros aplicados.
5. Atleta seleciona uma inscrição para visualizar os detalhes completos.

**Fluxo alternativo — nenhuma inscrição encontrada:**
- Sistema exibe mensagem informando que o atleta não possui inscrições cadastradas.

**Pós-condição:** Lista de inscrições do atleta exibida com os filtros aplicados.

---

### UC07 — Alocar Local

**Ator principal:** Organizador

**Pré-condição:** Organizador autenticado. Competição cadastrada. Local disponível no sistema.

**Fluxo principal:**
1. Organizador acessa o módulo de alocação de locais.
2. Seleciona a competição para a qual deseja alocar um local.
3. Visualiza a lista de locais disponíveis.
4. Seleciona o local desejado.
5. Sistema verifica a disponibilidade do local no horário da competição.
6. Sistema registra a alocação e associa o local à competição.
7. Sistema exibe confirmação da alocação.

**Fluxo alternativo — local indisponível no horário (passo 5):**
- Sistema exibe mensagem informando o conflito de horário com outra competição já alocada naquele local.
- Organizador escolhe outro local disponível e retorna ao passo 4.

**Fluxo alternativo — nenhum local disponível no horário:**
- Sistema informa que não há locais disponíveis para o horário da competição.
- Organizador pode alterar o horário da competição ou aguardar a liberação de um local.

**Pós-condição:** Local alocado à competição sem conflito de horário.

---

### UC08 — Verificar Disponibilidade de Local

**Ator principal:** Organizador

**Pré-condição:** Local e data/horário informados.

**Fluxo principal:**
1. Sistema recebe o local e o intervalo de data/hora a verificar.
2. Sistema consulta todas as competições já alocadas naquele local.
3. Sistema verifica se há sobreposição de horário com alguma competição existente.
4. Sistema retorna o resultado: disponível ou indisponível.

**Fluxo alternativo — local não possui competições alocadas:**
- Sistema retorna imediatamente como disponível.

**Pós-condição:** Resultado de disponibilidade retornado ao caso de uso chamador.

---

### UC09 — Liberar Local

**Ator principal:** Organizador

**Pré-condição:** Competição com status `CONCLUIDA` ou `CANCELADA` com local alocado.

**Fluxo principal:**
1. Organizador acessa o módulo de alocação de locais.
2. Filtra as competições concluídas ou canceladas com locais ainda alocados.
3. Seleciona a competição desejada.
4. Seleciona a opção "Liberar Local".
5. Sistema solicita confirmação.
6. Organizador confirma.
7. Sistema desvincula o local da competição.
8. Sistema marca o local como disponível para novas alocações.
9. Sistema exibe confirmação da liberação.

**Fluxo alternativo — competição ainda em andamento ou agendada:**
- Sistema bloqueia a liberação e exibe mensagem informando que o local só pode ser liberado após a conclusão ou cancelamento da competição.

**Pós-condição:** Local desvinculado da competição e disponível para novas alocações.

---

### UC10 — Registrar Resultado

**Ator principal:** Juiz

**Pré-condição:** Competição com status `EM_ANDAMENTO`. Pelo menos três atletas inscritos na competição.

**Fluxo principal:**
1. Juiz acessa o módulo de resultados.
2. Seleciona a competição para registrar o resultado.
3. Sistema exibe a lista de atletas inscritos na competição.
4. Juiz informa o atleta classificado em primeiro lugar.
5. Juiz informa o atleta classificado em segundo lugar.
6. Juiz informa o atleta classificado em terceiro lugar.
7. Sistema valida se os três atletas selecionados estão inscritos na competição.
8. Sistema valida se os três atletas selecionados são distintos.
9. Sistema registra o resultado com os três classificados.
10. Sistema gera as medalhas de ouro, prata e bronze associadas aos respectivos atletas e países representados.
11. Sistema atualiza o status da competição para `CONCLUIDA`.
12. Sistema notifica automaticamente o `QuadroDeMedalhas` por meio do padrão Observer.
13. Sistema exibe confirmação do registro.

**Fluxo alternativo — atleta selecionado não está inscrito na competição (passo 7):**
- Sistema rejeita o registro e exibe mensagem indicando qual atleta não está inscrito.
- Juiz corrige a seleção e retorna ao passo 4.

**Fluxo alternativo — atleta selecionado repetido (passo 8):**
- Sistema rejeita o registro e exibe mensagem informando que o mesmo atleta não pode ocupar mais de uma posição.
- Juiz corrige a seleção e retorna ao passo 4.

**Fluxo alternativo — competição já possui resultado registrado:**
- Sistema exibe o resultado já registrado e bloqueia novo registro.

**Pós-condição:** Resultado registrado, três medalhas geradas, competição com status `CONCLUIDA` e quadro de medalhas atualizado.

---

### UC11 — Atualizar Quadro de Medalhas

**Ator principal:** Sistema

**Pré-condição:** Resultado registrado com os três classificados e medalhas geradas.

**Fluxo principal:**
1. `GerenciadorResultado` notifica todos os observers registrados passando o resultado como parâmetro.
2. `QuadroDeMedalhas` recebe a notificação via método `atualizar(resultado)`.
3. Sistema extrai as três medalhas do resultado recebido.
4. Para cada medalha, sistema identifica o país representado pelo atleta na inscrição correspondente.
5. Sistema incrementa o contador de medalhas do tipo correspondente, ouro, prata ou bronze, para o país.
6. Sistema recalcula o ranking de países com base nos critérios definidos.
7. Sistema mantém o quadro de medalhas atualizado a partir dos resultados e medalhas registrados.

**Fluxo alternativo — observer não está registrado:**
- `GerenciadorResultado` ignora observers não registrados e notifica apenas os ativos.

**Pós-condição:** Quadro de medalhas atualizado com os dados do novo resultado, ranking de países recalculado.

---

### UC12 — Gerar Relatório de Medalhas

**Ator principal:** Comitê Olímpico

**Pré-condição:** Ao menos uma competição concluída com resultado registrado.

**Fluxo principal:**
1. Comitê Olímpico acessa o módulo de relatórios.
2. Seleciona o critério de ordenação do relatório, como por ouro, por total de medalhas ou por país.
3. Sistema consulta o `QuadroDeMedalhas` com o critério selecionado.
4. Sistema organiza os dados de acordo com o critério escolhido.
5. Sistema gera o relatório com a classificação dos países e respectivas quantidades de medalhas de ouro, prata e bronze.
6. Sistema exibe o relatório na tela.

**Fluxo alternativo — nenhum resultado registrado (passo 3):**
- Sistema informa que não há dados suficientes para gerar o relatório.

**Fluxo alternativo — filtrar por país específico:**
- Comitê Olímpico informa um país para filtrar.
- Sistema exibe apenas as medalhas conquistadas por aquele país com o detalhamento por modalidade.

**Pós-condição:** Relatório de medalhas gerado e exibido ao Comitê Olímpico conforme critério selecionado.

---

## Diagramas

### Diagrama de Caso de Uso

Modela os atores do sistema, como Administrador, Atleta, Organizador, Juiz e Comitê Olímpico, e suas interações com os principais casos de uso relacionados ao gerenciamento de competições, inscrições, locais, resultados e relatórios.

<img width="600px" src="imagens/diagrama-de-caso-de-uso.png"/>

---

### Diagrama de Classes

Representa a estrutura do sistema com as classes do domínio (`Competicao`, `Modalidade`, `Atleta`, `Local`, `Inscricao`, `Resultado`, `Medalha`, `Pais` e `QuadroDeMedalhas`) e o pacote `observer`, que aplica o padrão Observer para atualização automática do quadro de medalhas.

<img width="600px" src="imagens/diagrama-de-classes.png"/>

---

### Diagrama de Pacotes

Organiza o sistema em pacotes lógicos — `apresentacao`, `aplicacao`, `dominio` e `infraestrutura` — seguindo uma arquitetura de monólito modular com separação de responsabilidades e dependências controladas entre os módulos.

<img width="600px" src="imagens/diagrama-de-pacotes.png"/>

---

### Diagrama de Componentes

Modela os componentes principais do SGO, incluindo interface web, controllers REST, DTOs, services de aplicação, módulos de domínio, portas de repositório, adaptadores de persistência, componentes transversais de infraestrutura e integração com banco de dados PostgreSQL.

<img width="100%" src="imagens/diagrama-de-componentes.png"/>

---

### Diagrama de Implantação

Ilustra a arquitetura física do sistema, mostrando a distribuição dos componentes entre os dispositivos dos usuários, o servidor da aplicação SGO e o servidor de banco de dados PostgreSQL, além das conexões realizadas via HTTPS, REST API, HTTP/JSON e JDBC.

<img width="100%" src="imagens/diagrama-de-implantação.png"/>

---

## Arquitetura

O SGO foi modelado seguindo uma arquitetura de **monólito modular**, organizada em pacotes lógicos com separação de responsabilidades entre apresentação, aplicação, domínio e infraestrutura.

| Pacote / Camada lógica | Responsabilidade |
|---|---|
| `apresentacao` | Agrupa interface web, páginas, cliente HTTP, controllers REST e DTOs de entrada e saída. |
| `aplicacao` | Contém services, casos de uso e portas responsáveis por coordenar os fluxos do sistema. |
| `dominio` | Contém entidades, enums, regras de negócio e o padrão Observer aplicado ao controle de resultados e ao quadro de medalhas. |
| `infraestrutura` | Contém persistência, segurança, configurações e integrações técnicas auxiliares. |

A dependência principal segue o fluxo `apresentacao` → `aplicacao` → `dominio`. O acesso à persistência é desacoplado por portas, enquanto a infraestrutura implementa os detalhes técnicos de armazenamento e integração.

Essa organização mantém o sistema como um único deploy de aplicação, caracterizando um monólito modular, mas evita acoplamento excessivo entre interface, regras de negócio e detalhes técnicos.

---

## Padrão de Projeto

O sistema aplica o padrão **Observer** no controle de resultados:

- `GerenciadorResultado` atua como **Subject**, mantendo uma lista de observers registrados.
- `ResultadoObserver` é a **interface** que define o contrato de atualização.
- `QuadroDeMedalhas` é o **Observer concreto** que reage automaticamente ao registro de um novo resultado, atualizando o ranking de medalhas por país sem acoplamento direto com o módulo de resultados.

Além disso, a organização arquitetural separa responsabilidades entre os pacotes de apresentação, aplicação, domínio e infraestrutura, reforçando o baixo acoplamento entre regras de negócio e detalhes técnicos.

---

## Estrutura do Repositório

```txt
sistema-gestao-olimpiadas/
├── README.md
├── imagens/
│   ├── diagrama-de-caso-de-uso.png
│   ├── diagrama-de-classes.png
│   ├── diagrama-de-pacotes.png
│   ├── diagrama-de-componentes.png
│   └── diagrama-de-implantação.png
└── codigos/
    ├── diagrama-de-caso-de-uso.puml
    ├── diagrama-de-classes.puml
    ├── diagrama-de-pacotes.puml
    ├── diagrama-de-componentes.puml
    └── diagrama-de-implantação.puml
```

---

## Como Visualizar os Diagramas

Os arquivos `.puml` podem ser visualizados de três formas:

**1. Online — PlantUML Web Server**  
Acesse [plantuml.com/plantuml](https://www.plantuml.com/plantuml), cole o conteúdo do arquivo `.puml` e clique em Submit.

**2. VS Code**  
Instale a extensão [PlantUML](https://marketplace.visualstudio.com/items?itemName=jebbs.plantuml) e use `Alt+D` para preview em tempo real.

**3. Plugin IntelliJ / PyCharm**  
Instale o plugin PlantUML Integration disponível no marketplace da JetBrains.

---

## Autores

| Nome | GitHub |
|---|---|
| Gabriel Pedrosa do Carmo Nonato | [GpNonato](https://github.com/GpNonato) |
| Pedro Henrique Silva Vargas | [PHnSilva](https://github.com/PHnsilva) |

---

> Trabalho 1 — Projeto de Software · Engenharia de Software · Professor João Paulo Carneiro Aramuni
