# Mundo Simulado — documento de design

**Nome de trabalho:** *Crônica* (provisório)

**Local:** `C:\dev\chronicle`, projeto separado. Reaproveita código do Ossuary por cópia e adaptação. Não depende da pasta do Ossuary para compilar ou rodar.

**Repositório:** https://github.com/Bruno-BRG/chronicles

**Referências principais:** Dwarf Fortress (seção 3.1) e RimWorld (seção 3.2).

**Status:** rascunho v0.5 para revisão. Nada foi implementado nem copiado.

**Data:** 2026-10-08

---

## 1. A ideia

Um mundo que se conta sozinho. Antes de qualquer pessoa chegar, um mundo inteiro já tem história: povos que nascem, guerreiam e somem, figuras que vivem e morrem, sítios que viram ruína, objetos que mudam de mãos. Então um grupo fundador de oito pessoas chega a um vale desse mundo. Ninguém controla essas pessoas. Cada uma é uma entidade com corpo, necessidades, pensamentos, personalidade, profissão e relações, e decide o que fazer a cada hora simulada.

O observador só assiste. Pode pausar, acelerar, seguir alguém e ler o que aconteceu, inclusive a história do passado. Com o tempo surgem família, conhecimento, normas, propriedade, liderança, assentamentos, crenças e conflitos. A referência principal é o Dwarf Fortress, com ideias do RimWorld para a vida interna das pessoas: quebras, interações, passados e traços.

---

## 2. Experiência alvo

O que quem assiste deve sentir:

- Curiosidade sobre o que vem a seguir, sem roteiro.
- Afeição por pessoas específicas, não por "unidades".
- Surpresa: decisões que só fazem sentido depois de ver a história inteira.
- Um vale com passado: o grupo chega a um lugar que já teve dono, e os restos disso estão lá.
- Um livro vivo: a crônica se escreve enquanto o mundo roda.

Exemplos ilustrativos. Não são conteúdo fixo, são o tipo de frase que o sistema deve produzir:

> **Ano 1, inverno, dia 9.** Bento adoece e não consegue se levantar. Sofia passa a noite ao lado dele.
>
> **Ano 2, primavera.** Dois jovens passam a dormir sob o mesmo abrigo. O grupo ainda não tem uma palavra para isso.
>
> **Ano 3, verão.** Pela primeira vez, alguém acende fogo de propósito. Quem ensinou foi Tomé, morto no inverno anterior.
>
> **Ano 4, outono.** Na beira do rio, o grupo encontra uma tumba com uma espada. A lenda diz que ela foi forjada por Marra, da casa dos Tiloques, que morreu na guerra com os Sarkan, há 212 anos.
>
> **Ano 6, inverno.** Na ruína de um templo, Sofia encontra uma tábua de argila. Alguém gravou ali a praga que atingiu o povo dos Sarkan e a erva que salvou metade das pessoas. Sofia leva a tábua para o grupo.

---

## 3. Referência e princípios

### 3.1 Dwarf Fortress é a referência principal

Dwarf Fortress é a inspiração principal. Quando uma decisão de design estiver em dúvida, a pergunta é: "o que o Dwarf Fortress faria?" A resposta vale, a menos que contrarie um princípio deste documento.

O que copiamos, como mecânica e ideia de design:

| Área | O que pegamos do Dwarf Fortress | Onde aparece aqui |
|---|---|---|
| Construção de mundo | Terreno com geologia, biomas, rios e montanhas, gerado antes de qualquer história | Seções 6.2 e 6.4 |
| História procedural | Séculos de história gerados antes do início: civilizações, figuras, guerras, sítios, ruínas, artefatos | Seção 6.6 |
| Lendas | Uma história consultável: figuras, sítios e artefatos têm páginas com o que aconteceu | Seções 6.7 e 11 |
| Profundidade de personagem | Facetas de personalidade, valores, preferências e relações pessoais com memória | Seções 7.3, 7.4 e 7.5 |
| Pensamentos e humor | Um fluxo de pensamentos com peso que decai; o humor é a soma deles | Seção 7.6 |
| Liberdade | Ninguém recebe ordens. Cada pessoa escolhe o que fazer por necessidade, gosto e humor | Seções 7.7 e 7.8 |
| Profissões | Habilidades que sobem com a prática e enferrujam sem uso. Ofício preferido e ofício bom não são a mesma coisa | Seção 7.7 |
| Estados extremos | Quebras mentais e inspiração criativa, quando o humor e a personalidade chegam a um extremo | Seção 7.10 |
| Artefatos | Objetos feitos num momento de inspiração, com nome, autor e histórico de donos | Seções 5.2 e 6.7 |
| Simulação viva | Clima, estações, plantas, fauna e ecologia que continuam rodando | Seção 6 |
| Doenças e contágio | Doenças com sintomas por estágio, contágio e imunidade; surtos que atravessam o grupo | Seções 7.1 e 6.6 |
| Escrita e registros | Livros, tábuas e inscrições que citam fatos reais; quem lê aprende o que outro registrou | Seções 8 e 9 |
| Arte que retrata fatos | Pinturas, gravações e esculturas de eventos reais, que espalham memórias | Seções 6.7 e 8 |
| Migrantes | Gente de fora que chega ao vale, com passado e saberes próprios | Seções 6.8 e 8 |
| Zonas e cômodos com valor | Depósitos com função; cômodos que valem mais por móveis e comida | Seção 8 |

Dwarf Fortress não é open source. Copiamos mecânicas e ideias, não código nem textos do jogo. O código que reaproveitamos é o do Ossuary, que é nosso.

O Dwarf Fortress levou décadas de desenvolvimento. Por isso a v1 pega o núcleo de cada área (coluna "Onde aparece") e deixa o resto para a seção 15, em Opcional.

### 3.2 RimWorld é a segunda referência

O RimWorld entra para a vida interna das pessoas: quebras, interações, passado e traços. O Dwarf Fortress continua mandando na história e no mundo.

| Área | O que pegamos do RimWorld | Onde aparece aqui |
|---|---|---|
| Histórico de vida | Cada pessoa tem um passado: origem, ofício anterior, perdas e marcas | Seção 7.2 |
| Quebras mentais em três níveis | Quebras menores, maiores e extremas, cada uma com tipos próprios | Seção 7.10 |
| Interações sociais com tipos | Conversa casual, conversa profunda, insulto, cortejo e briga, com sucesso que depende de sociabilidade e relação | Seção 7.9 |
| Paixão por habilidade | Nenhuma, pouca ou muita paixão, que multiplica aprendizado e satisfação | Seção 7.7 |
| Traços incomuns | Piromania, gulodice, ganância: traços discretos com comportamentos próprios | Seção 7.3 |
| Ideias culturais que se espalham | Memes e preceitos com efeito, que se espalham por imitação e podem ser abandonados | Seção 8 |
| Cuidado de ferido e próteses | Ferido é tratado; membro perdido vira prótese | Seções 7.1 e 9 |

O RimWorld também tem um diretor de eventos (o "storyteller"), que escolhe quando atacar. Não pegamos isso, porque contradiz o princípio de emergência sem roteiro. Quem faz o papel de ritmo é o mundo, na seção 6.8.

### 3.3 Princípios

1. **Observar, não controlar.** Nenhuma ação do observador altera o estado da simulação. A entrada se limita a pausa, velocidade, câmera, seleção, leitura de lendas e semente.
2. **Emergência, não roteiro.** Nenhum estágio é disparado por script ("agora, a agricultura"). Marcos são *detectados* no estado do mundo, nunca *acionados*. A história procedural segue a mesma regra: os eventos saem de regras e de sorteios da semente, nunca de um roteiro escrito.
3. **Toda entidade é uma mente.** Cada pessoa decide sozinha com base no próprio estado, no que sabe e no que sente. Animais têm uma mente mais simples, mas também decidem.
4. **Mesma semente, mesma história.** O mundo inteiro, o passado e o presente são função da semente. Compartilhar uma semente é compartilhar uma história.
5. **O mundo lembra.** Toda coisa relevante deixa rastro: na memória de alguém, no mapa, em uma lenda, num registro escrito ou na crônica.
6. **Mundo primeiro, linguagem depois.** Nenhuma IA de linguagem fica no caminho crítico da simulação. Texto rico é uma camada por cima.
7. **Isolamento.** Este projeto não depende de nenhum arquivo fora de `C:\dev\chronicle` para compilar ou rodar. O repositório do Ossuary não recebe nada daqui: nem código, nem documentação, nem mudança de comportamento ou de formato de save.
8. **Reuso sem reverência.** O Ossuary é ponto de partida, não contrato. Copiamos o que funciona e adaptamos livremente. Não preservamos a estrutura nem a compatibilidade dele.
9. **Pressão vem do mundo, sem diretor.** Seca, praga, guerra e migração saem de condições do mundo e de sorteio da semente. Nenhum diretor escolhe quando acontecem (seção 6.8).

---

## 4. Escopo

### 4.1 Dentro da v1

- Mundo histórico com 2 a 4 povos, gerado com terreno, biomas e rios.
- História procedural de 300 a 500 anos, antes da chegada do grupo.
- Lendas consultáveis: figuras, sítios, guerras e artefatos com páginas próprias.
- Uma região viva de ~96 × 96 tiles, com ruínas e tumbas herdadas da história.
- Grupo fundador de 8 pessoas, com idades de 6 a 58 anos, sem tecnologia. Cada uma com histórico de vida ligado à história do mundo.
- Facetas, valores, traços incomuns, paixões por habilidade, necessidades, preferências, pensamentos e humor.
- Liberdade de escolha, sem ordens, com interações sociais de tipos diferentes e quebras mentais em três níveis.
- Doenças com contágio, surtos e imunidade. Cuidado de ferido.
- Fauna com ecologia simples, clima e estações.
- Nascimento, envelhecimento, morte e família.
- Descoberta e transmissão de conhecimento e de ofícios.
- Escrita e registros, com saberes que sobrevivem a quem os tinha. Obras de arte que retratam fatos reais.
- Ideias culturais que se espalham por imitação.
- Grupos emergentes (bandos), normas, propriedade simples e liderança por influência.
- Migrantes e refugiados que chegam ao vale.
- Zonas de armazenamento e cômodos com valor.
- Assentamento permanente, armazenamento e agricultura básica.
- Pressões do mundo: seca, inverno ruim, enchente, praga, guerra e migração.
- Crônica bilíngue (EN e PT) da região viva.
- Visualizador somente leitura, com seleção de pessoa, painel de grupo, crônica e lendas.

### 4.2 Fora da v1 (não-metas)

- Qualquer controle ou intervenção do observador. Nada de "poderes de deus". Pode virar modo opcional depois.
- Diretor de eventos, o "storyteller" do RimWorld. Contradiz "emergência, não roteiro". Quem faz o papel é o mundo (seção 6.8).
- Controle de prioridades por pessoa, como no Dwarf Fortress ou no RimWorld. Conflita com "observar, não controlar".
- Drogas e vício em detalhe. Bebida fermentada entra como prazer, sem dependência (seção 7.4).
- Combate tático com formação.
- Herói, missões, combate de RPG e a camada de jogo do Ossuary.
- Mais de um mundo, multiplayer.
- Magia e raças fantásticas (ver perguntas em aberto).
- Criaturas lendárias, como megafauna e bestas esquecidas (ver perguntas em aberto).
- Camadas subterrâneas, minas e cavernas (ver perguntas em aberto).
- Genética detalhada. Na v1, herança simples de traços com mutação.
- Diálogo gerado por LLM no caminho crítico.
- Gráficos 3D ou sprites. Mantém o visual "Phosphor & Bone" de terminal.

---

## 5. Arquitetura

### 5.1 Pastas

| Pasta | Papel | Notas |
|---|---|---|
| `src/Chronicle/` | A biblioteca da simulação. Reúne código copiado do Ossuary e código novo, organizado por sistema (ver abaixo) | .NET 10, como o host do Ossuary (a confirmar no F0). Nunca usa nada de `Game` |
| `src/Chronicle.Host/` | Host JSON sobre stdin/stdout, como o `Ossuary.Desktop` | Operações: `new`, `tick`, `speed`, `pause`, `frame`, `inspect`, `legend`, `chronicle` |
| `src/Chronicle.Headless/` | Testes, soak de sementes, bot de métricas, dumps ASCII | Mesmo papel do `Ossuary.Headless` |
| `viewer/` | Shell Tauri do visualizador, com o renderer copiado de `desktop/src` | Nenhuma regra de jogo aqui |

Organização por sistema dentro de `src/Chronicle/`:

- `Base/`: aleatoriedade, mapa, campo de visão, pathfinding, paleta, textos bilíngues, geração de nomes.
- `World/`: geologia, biomas, rios, clima, fauna, recursos e pressões do mundo.
- `History/`: simulação histórica anual (civilizações, figuras, sítios, guerras, artefatos, registros e obras da história) e lendas.
- `Mind/`: histórico de vida, facetas, valores, traços incomuns, paixões, necessidades, pensamentos, humor, decisão, interações e quebras mentais.
- `Body/`: corpo, ferimentos, doenças e contágio, cuidado, próteses, dano e combate.
- `Economy/`: ofícios, habilidades, receitas, fabricação, coleta, mercado, regateio, caravanas, zonas e cômodos.
- `Society/`: bandos, relações, liderança, propriedade, dívida, facções, saques e migrantes.
- `Culture/`: crenças, ideias culturais, normas, mitos, arte, escrita e ritos.

Todos podem usar `Base/`. Nenhum sistema depende de `Game`, porque `Game` é o estado de um herói do Ossuary.

#### 5.1.1 Como trazer código do Ossuary

- **Ctrl-C, Ctrl-V e adaptar.** Copiamos o arquivo e mudamos o que for preciso: nomes, namespace, tipos, dependências de `Game` e de `Player`. A estrutura do Ossuary é referência, não contrato.
- **Custo real.** Arquivo copiado com referências a `Game` ou `Player` exige adaptação. Por isso o ganho vem primeiro dos sistemas menos acoplados. Um sistema que custar mais para adaptar do que para escrever do zero é reescrito.
- **Origem:** commit `f1e320e` do Ossuary, não o diretório de trabalho. O working tree tem alterações em andamento, e copiar dele traria código inacabado.
- **Licença:** o Ossuary é MIT, com copyright de Bruno-BRG. Cada arquivo copiado mantém o aviso de copyright no topo, e o texto da licença fica em `LICENSE-OSSUARY.txt`, na raiz do projeto.
- **Registro:** `THIRD_PARTY.md` lista cada arquivo copiado, o caminho de origem e um resumo do que mudou. Serve para saber de onde veio o código, não para sincronizar.
- **Sem sincronização.** Correções feitas no Ossuary não chegam aqui sozinhas. Se algo valer a pena, você decide caso a caso.

### 5.2 O que trazer do Ossuary

Lista preliminar, por sistema. Os caminhos são de `engine/Ossuary.Core/`, exceto quando indicado. A coluna "Fase" usa a numeração da seção 15. Linhas marcadas como "novo" não têm equivalente no Ossuary; o que existe lá serve só de modelo parcial.

**Renderização e visual**

| Sistema | Origem | O que aproveitamos | O que muda | Fase |
|---|---|---|---|---|
| Renderização | `desktop/src/renderer.ts`, `font.ts`, `style.css` | Terminal de bitmap 8×16, cores, grade | Quase nada: troca o frame de entrada | F1 (ASCII), F9 |
| CRT | `desktop/src/crt.ts` | Linhas de varredura, brilho, glow | Só ajustes de cor | F9 |
| Paleta | `Theme.cs` | Phosphor & Bone | Nova paleta só se o visual pedir | F1 |
| Composição de telas | `TextBuilder.cs`, `Loc.cs` | Telas como dados, texto em EN e PT | Remover o acoplamento a `Game` | F1 |
| Efeitos e sons (opcional) | `desktop/src/fx.ts`, `anim.ts`, `audio.ts`, `stingers.ts` | Efeitos visuais de evento; sinais musicais | Ligar aos eventos da crônica e das lendas | F9 |

**Corpo e dano**

| Sistema | Origem | O que aproveitamos | O que muda | Fase |
|---|---|---|---|---|
| Corpo e ferimentos | `Combat/Body.cs`, `Game.Wounds.cs` | Partes do corpo, sangramento, cura, cicatriz, curativos | Estado da pessoa no lugar do herói | F4 |
| Combate | `Combat/Combat.cs` | Acerto, dano, morte | Encontro por tick, não por golpe | F4 |
| Próteses | `Combat/Body.cs` (membros perdidos, "severed") | Membro perdido que deixa de ser usado | Prótese de madeira ou metal; novo | F5 |
| Doenças e contágio (novo) | Modelo parcial: dano por tipo e resistência a veneno (`Entities/Actor.cs`, `Entities/Player.cs`) | Dano por tipo, com resistência a cada tipo | Estágios, contágio por ar, contato, água ou ferida, imunidade; novo | F4 |
| Fauna | `Entities/Bestiary.cs` | Tabela estática de espécies, com faixas de aparição e pesos | Só as espécies do mundo; os pesos passam a vir da ecologia (seção 6.5) | F1 |

**História, lendas e artefatos**

| Sistema | Origem | O que aproveitamos | O que muda | Fase |
|---|---|---|---|---|
| Motor de história | `World/History.cs` | Listas de epítetos, lugares, casas e papéis; frases bilíngues de eventos | O motor atual sorteia figuras, casas e eventos a partir de listas e frases prontas. Ele vira simulação anual de atos, como no Dwarf Fortress. A classe `Chronicle` precisa de outro nome, para não colidir com o nome do projeto | F2 |
| Lendas | `Game.Legends.cs` | O passado aprendido aos poucos: crônicas, livros, boatos, canções, biografias de relíquias, gravações e túmulos | Vira páginas consultáveis de figuras, sítios e guerras | F2 |
| Inscrições e obras da história | `Game.Places.cs` (gravações antigas que contam a crônica, túmulos e o que cada sala foi) | Textos gravados em pedra que citam fatos | Inscrições e obras que sobram nas ruínas e nas salas | F2 |
| Nomes de lugares | `Game.Legends.cs` (`NamePlaces`: ruínas levam o nome do que aconteceu ali); `Loc.Names.cs` (nomes em PT, com gênero) | Ruína que leva o nome do evento que a deixou | Gerador de nomes por povo, com sílabas, é novo: não há equivalente no Ossuary | F2 |
| Artefatos com história | `Items/Masterworks.cs`, `History.Biography`, `Item.Owners`, `Item.Deeds` (descritos em `docs/design/systems.md`) | Objetos com nome, autor, donos e feitos | Vira o sistema de artefatos: inspiração gera artefato, e cada dono é um registro | F5 |
| Obituários | `Morgue.cs` (registro de partidas encerradas, como dados simples) | Formato de registro com causa e resultado | Um obituário por morte, montado a partir do log da pessoa | F4 |
| Boatos | `Rumours.cs`, `Game.Rumours.cs` | Boato com confiabilidade por temperamento | Usa as facetas da seção 7.3 | F6 |
| Eventos e pressões do mundo | `Game.Events.cs`, `Game.Raids.cs` | Eventos com consequência; ataques a um lugar | Condições do mundo e sorteio, sem diretor (seção 6.8) | F1, F6, F8 |
| Registro de atos | `Game.Ledger.cs` | Registro só de acréscimo, com os feitos que o mundo deve lembrar | Base do registro detalhado da crônica | F6 |
| Histórico de vida | `Bones.cs` (`Legend`), `Persona.cs` (`Want`) | Feitos de quem já viveu; desejo de cada pessoa | Passado gerado a partir da história do mundo (seção 7.2) | F3 |

**Ofícios, mercado e economia**

| Sistema | Origem | O que aproveitamos | O que muda | Fase |
|---|---|---|---|---|
| Ofícios e receitas | `Items/Trades.cs`, `Game.Crafting.cs` | Receita como dado, nível de ofício e qualidade | Receitas pré-históricas novas. Escala de habilidade com mais degraus | F5 |
| Escrita | `Items/Trades.cs` (escriba: pergaminho, tinta, pergaminhos escritos); `Game.Legends.cs` (crônicas e livros em estantes, como modelo) | Ofício e materiais de escrita | Escrita como marco, com registros que sobrevivem (seção 9) | F5 |
| Arte e música | `Items/Trades.cs` (músico, luteiro); `Game.Gathering.cs` (música); `Game.Places.cs` (gravações) | Ofícios de arte e música, e gravações em pedra | Obras que retratam fatos (seção 8) | F5 |
| Coleta | `Game.Gathering.cs` | Coleta por tipo de terreno e tempo gasto | Coleta por tile e estação | F3 |
| Mercado | `Game.Market.cs` | Memória de vendas por tipo de mercadoria; excesso de oferta que se desfaz com o tempo | Preço por bando ou assentamento, não por cidade | F7 |
| Regateio | `Game.Haggle.cs` | Negociação que depende do humor e da memória de quem negocia | Troca entre pessoas e entre bandos | F7 |
| Caravanas | `Game.Caravans.cs` | Grupos que passam pela região, com mercadoria | Contato entre bandos e forasteiros | F7 |
| Zonas e cômodos com valor | `GameMap.Rooms`, `RoomAt`, `Gen/DungeonGen.cs` | Salas com função, reconhecidas pelo mapa | Depósitos e cômodos com valor por móveis e comida | F7 |
| Saques | `Game.Raids.cs` | Ataque a um lugar, com perdas | Disputa por recurso entre bandos | F8 |

**Pessoas, relações e mundo**

| Sistema | Origem | O que aproveitamos | O que muda | Fase |
|---|---|---|---|---|
| Personalidade | `Persona.cs` | Oito traços, um desejo (`Want`), um segredo e a marca de problema pessoal (`Troubled`) | Ampliado para facetas, valores e traços incomuns (seção 7.3) | F3 |
| Paixão por habilidade (novo) | `Entities/Progression.cs` (perks por nível) como modelo parcial | Escolhas com pré-requisito de nível, habilidade ou outra escolha | Nível de paixão: nenhuma, pouca ou muita (seção 7.7) | F3 |
| Interações sociais | `TownText.cs` (falas como dados, com português ao lado) | Falas de conversa, escritas uma vez em EN e PT | Tipos de interação com sucesso variável (seção 7.9) | F3 |
| Ideias culturais | `Entities/Gods.cs` (gostos, desgostos, bênçãos) | Preferências coletivas com efeito | Ideias que se espalham e podem ser abandonadas (seção 8) | F6 |
| Facções | `Game.Factions.cs` | Quem é rival de quem | Relações entre bandos, não facções fixas | F8 |
| Migrantes | `Game.Travellers.cs` (peregrino, refugiado) | Gente de fora que passa pelas estradas | Chegadas de gente com passado e saberes próprios | F8 |
| Mapa, visão e caminhos | `GameMap.cs`, `Tile.cs`, `Fov.cs`, `Pathfinder.cs` | Grade, visão com sombra, A* e flow field | Quase nada | F0 |
| Aleatoriedade | `Rng.cs` | xoshiro256**, `Fork`, `FromString` | Um fluxo por subsistema (seção 5.4) | F0 |
| Terreno | `World/OverworldGen.cs`, `World/WorldGen.cs` | Regiões, terreno, rios | Mundo histórico grande e região viva (seção 6.1) | F1 |
| Materiais | `Items/Materials.cs`, `Items/Catalogue.cs` | Pedra, madeira, metais, peso | Só o que o mundo tem. Metais ficam na fase opcional | F1 |

Ordem: começamos pela base e pelo renderer (F0 e F1), que não dependem de nada. Depois vêm o mundo, a história e as pessoas (F1 a F3), e então corpo, ofícios, grupos e economia. Cada peça copiada passa por uma pergunta: qual decisão da simulação ela ajuda a tomar? Se não há resposta, ela não entra.

### 5.3 Tempo

- **1 tick = 1 hora simulada na região viva.** 24 ticks = 1 dia. 90 dias = 1 estação. 360 dias = 1 ano (8.640 ticks).
- **Passo anual no mundo histórico.** A história avança por ano, e cada ano processa os atos das figuras e dos povos (seção 6.6).
- Um tile ≈ 100 m (a calibrar). Deslocamento médio em terreno plano ≈ 20 tiles por hora (a calibrar).
- Ação atômica por tick ou com duração em ticks: colher 2–4, caçar 1–6, construir dias. Combate se resolve por encontro, não por golpe.
- **Velocidades do observador:** pausa, 1×, 4×, 16×, 64×, 256×, máximo. 1× ≈ 1 tick por segundo, ou 24 segundos por dia. A velocidade muda só o tempo de parede, nunca o resultado.
- **Decisão orientada a evento.** Uma pessoa reavalia o que fazer só quando (a) a ação termina, (b) uma necessidade cruza um limiar, (c) algo novo entra na percepção, (d) alguém pede algo ou (e) um pensamento forte aparece. Não se pensa a cada tick.
- **Orçamento por tick.** Número máximo de decisões e de caminhos por tick. O excedente fica numa fila ordenada por id, com início rotacionado a cada tick. É determinístico e evita picos de CPU.

Ordem de um tick na região viva:

1. Relógio: hora, dia, estação, ano.
2. Ambiente: clima, pressões do mundo, eventos e rebrota diária.
3. Percepção e memória.
4. Pensamentos e humor: entram novos pensamentos, os antigos decaem.
5. Decisões das pessoas e animais que precisam, dentro do orçamento.
6. Movimento e resolução das ações.
7. Passe social diário: vínculos, interações, boatos, ensino, normas.
8. Passe de vida: idade, nascimentos, mortes, doenças e contágio.
9. Detectores: bandos, propriedade, assentamento, marcos. Saem para a crônica.
10. Checkpoint anual e hash de estado.

### 5.4 Determinismo

- Um `Rng` por subsistema, derivado da semente com `Fork` ou com hash, por exemplo `seed ^ hash("terreno")`. Assim, mudar a fauna não muda o terreno nem a história.
- Estado da simulação em **inteiros ou ponto fixo**: necessidades de 0 a 1000, afinidade de −1000 a 1000, humor e pensamentos com a mesma escala. Isso evita diferenças de ponto flutuante entre máquinas.
- Proibidos: `DateTime`, iteração de `Dictionary` sem ordem definida, `GetHashCode` de string.
- **Auditoria do código copiado.** Antes de entrar, cada trecho copiado passa por essa lista: `Rng` global, `DateTime` e `Dictionary` iterado são trocados pelas regras acima.
- **Hash de estado** em cada checkpoint, do passado e do presente. Teste de regressão com semente fixa e hash dourado. Se a regra mudar, o hash muda e a versão sobe, como o `SaveStore.Version` do jogo.
- Semente vai como string decimal no protocolo. Um uint64 não pode passar por `Number` no JSON (regra que o Ossuary já usa, em `AGENTS.md`).
- **Sem gravação de teclas.** Diferente do jogo, não há entrada do jogador. A história é função da semente e da versão. Salvar significa guardar checkpoints para retomar rápido.

---

## 6. O mundo e sua história

### 6.1 Duas escalas

- **Mundo histórico:** mapa grande, ~128 × 128 (a calibrar), onde os povos existem, lutam e somem. Roda em anos.
- **Região viva:** recorte de ~96 × 96 tiles dentro do mundo, onde o grupo fundador chega. Roda em horas.

A região viva é escolhida pelo gerador, perto de recursos e de ruínas. Cada tile dela vem do terreno do mundo histórico. Por isso, as ruínas, os caminhos e as fronteiras de antes estão lá, no mesmo lugar.

### 6.2 Terreno e região

- Geologia e biomas gerados com ruído próprio sobre a base de `OverworldGen` copiada: rio, lago, margem, planície, floresta, colinas, montanhas, rochedos com pedra e minério, pântano e um trecho de clima mais duro.
- Água é o recurso mais importante: bebida, peixe, argila e transporte.
- A região viva tem uma entrada. Onde o grupo chega é decidido pelo gerador, não pelas pessoas.

### 6.3 Recursos por tile

| Recurso | Fonte | Regeneração |
|---|---|---|
| Frutas e raízes | Floresta, campo | Sazonal, lenta |
| Caça | Animais | Reprodução do animal |
| Peixe | Água | Constante, limitada pela pesca |
| Madeira | Floresta | Não rebrota no curto prazo |
| Pedra | Rochedos | Não rebrota |
| Argila | Margens de rio | Lenta |
| Minério | Colinas | Não rebrota (fase opcional) |
| Água | Rios, lagos, poços | Constante |

### 6.4 Clima e estações

- Quatro estações. O frio aumenta a necessidade de abrigo e fogo. O verão aumenta as frutas. O inverno reduz caça e colheita.
- Eventos: chuva, tempestade (derruba abrigo fraco), seca, cheia. São sorteados pela semente e pela estação, nunca pelo relógio de parede. As pressões mais graves do mundo estão na seção 6.8.
- O clima também roda no mundo histórico, em escala anual, e pode ter pesado na queda de um povo.

### 6.5 Fauna e ecologia

- Presas: cervos, coelhos, aves, peixes. Predadores: lobos, ursos. Carniça.
- Capacidade de suporte por tile. Presas só se reproduzem onde há pasto, e predadores dependem delas. As oscilações populacionais aparecem sem script.
- Animais têm mente instintiva: fome, medo, reprodução e território. Não têm memória social.
- Domesticação (cão de companhia, depois cabra ou ovelha) é fase tardia. É o sinal de que a relação pessoa–animal virou costume.

### 6.6 História procedural

A história é gerada antes da chegada do grupo, em passos anuais, no mundo histórico. São regras e sorteios da semente, não um roteiro.

- **Povos:** de 2 a 4 povos, cada um com território, recursos, valores e tecnologia de partida. Nascem, crescem, dividem-se e somem.
- **Figuras históricas:** pessoas notáveis, com nome, idade, ofício, família e morte. Usam um modelo anual simples: nascem, casam, têm filhos, fazem atos e morrem. A mente completa (seção 7) fica para as pessoas vivas da região viva.
- **Atos:** a cada ano, figuras e povos produzem atos. Fundar um sítio, declarar guerra, vencer uma batalha, casar, fazer um artefato, criar um mito, morrer. Cada ato tem causa e consequência registradas.
- **Sítios:** vilas, fortalezas, templos, cemitérios. Quando o povo cai, o sítio vira ruína e a ruína aparece no mapa da região viva, se estiver nela.
- **Guerras e disputas:** surgem de recurso escasso, rancor entre líderes e fronteiras. Terminam por vitória, acordo ou extinção.
- **Mitos:** um povo pode criar deuses, figuras sagradas e histórias de origem. Eles se espalham por imitação, como na seção 8.
- **Registros e obras:** povos escrevem, gravam e pintam fatos: guerras, mortes de chefes, pragas, receitas. Parte desses objetos sobrevive nas ruínas (seção 6.7).
- **Doenças:** pragas surgem em um povo ou em uma cidade, espalham-se por rios, rotas de comércio e guerras, e podem derrubar um povo inteiro.
- **Escala:** 300 a 500 anos. Com algumas centenas de figuras, o processo cabe em poucos segundos.

Resultado: um catálogo de figuras, sítios, guerras, artefatos, mitos, registros e obras, com páginas consultáveis (seção 6.7).

### 6.7 Sítios, artefatos e lendas

- **Lendas consultáveis:** toda figura, sítio, guerra, artefato, mito, registro e obra tem uma página. A página de uma figura lista nascimento, ofícios, casamentos, atos e morte. A de um sítio lista quem o fundou, quem o destruiu e quando.
- **Artefatos com nome:** um artesão com habilidade alta pode ter uma inspiração (seção 7.10) e produzir um artefato único, com nome próprio, material e autor. O artefato passa de dono em dono, e cada dono fica registrado.
- **Ruínas e tumbas:** a região viva herda ruínas e tumbas do mundo histórico. Quem as visita encontra objetos e registros do passado. O grupo fundador chega a um lugar que já teve dono.
- **Fontes da lenda:** escrita, arte e gravações encontradas nas ruínas viram páginas e pistas. Uma gravação na pedra pode citar uma guerra que nenhuma figura da região viva conhece, e o grupo descobre isso lendo.
- **Nomes:** sítios, figuras, artefatos e mitos recebem nomes gerados pela cultura do povo. Cada povo tem um padrão de sílabas, e o padrão muda com o tempo.

### 6.8 Pressões do mundo

O mundo empurra a vida do grupo, sem diretor. Cada pressão tem uma condição, uma chance e um efeito. As condições vêm do próprio mundo: clima, povos vizinhos, rotas e recursos.

| Pressão | Condição | Efeito na região viva |
|---|---|---|
| Seca | Duas estações de chuva abaixo da média | Menos água e menos fruta por um ano; animais migram |
| Inverno ruim | Temperatura abaixo do limite por mais de uma estação | Caça cai; abrigo fraco não aguenta; humor cai |
| Enchente | Chuva forte sobre margem baixa | Perde-se estoque e sítio ribeirinho |
| Praga | Surto no povo vizinho ou numa rota de rio e comércio | Doença chega por contato, por migrante ou pela água |
| Guerra | Povo vizinho com recurso escasso e líder com rancor | Saques, refugiados e cisão |
| Migração | Povo que caiu ou perdeu terra | Refugiados chegam com saber, rancor ou esperança |

Cada pressão é sorteada pela semente, com a chance ajustada pelas condições. A chance sobe quando as condições se somam (seca e praga juntas, por exemplo). Nada é marcado para um dia específico. Há um limite de pressões ao mesmo tempo, para o grupo não ser esmagado de uma vez.

---

## 7. As pessoas

### 7.1 Corpo

- Idade em ticks, convertida em ano e dia. Estágios: criança (0–12), jovem (13–17), adulto (18–55), idoso (56+). Cada estágio muda o que a pessoa consegue fazer.
- Saúde, fome, sede, sono, temperatura e ferimentos (a partir de `Body.cs` copiado).
- **Doenças com contágio:** cada doença tem sintomas por estágio, uma forma de contágio (ar, contato, água ou ferida) e uma imunidade que pode sobrar depois da cura. Surtos se espalham entre vizinhos, por rio e por rota de comércio. Cuidar de doente, isolar e enterrar viram comportamentos que o grupo aprende ou inventa.
- **Cuidado de ferido:** a ação "cuidar" aplica curativo, reduz sangramento e acelera a cura. Quem tem habilidade de cura faz melhor, e quem foi cuidado guarda memória de quem ajudou.
- **Próteses:** um membro perdido pode ser substituído por prótese de madeira ou metal, feita por quem tem ofício de fabricação. A prótese muda o que a pessoa consegue fazer e entra no humor. Vem na fase 5, porque depende de fabricação.
- Causas de morte: velhice, fome, sede, frio, doença, ferimento, predador, violência, parto. Toda morte gera um obituário.

**Corpo não é cultura.** Ninguém nasce sabendo acender fogo. Todo mundo nasce sabendo andar, comer, reconhecer rostos, sentir medo e chorar. O que é cultural precisa ser aprendido ou inventado.

### 7.2 Histórico de vida

Cada pessoa chega ao presente com um passado, gerado a partir da história do mundo. Os fundadores são sobreviventes de algum povo que existiu no mundo histórico. Quem nasce no vale tem o passado começando nos pais.

O passado tem quatro partes:

- **Origem:** de que povo ou lugar veio, com a língua e o padrão de nome que carrega.
- **Ofício anterior:** o que fazia antes, com a habilidade inicial que trouxe.
- **Perdas:** quem morreu ao redor e em que circunstância. Cada perda vira um pensamento de longa duração (seção 7.6).
- **Marca:** algo que a pessoa carrega, físico (cicatriz, objeto herdado) ou de fama (ser filha ou filho de alguém conhecido).

A origem liga a pessoa às lendas. Se o pai dela aparece numa lenda como guerreiro, a página da lenda cita a pessoa, e outras pessoas do vale podem ouvir isso.

### 7.3 Facetas, valores e traços incomuns

Cada pessoa tem três conjuntos de características. Nenhuma é um rótulo de texto: cada uma é um número ou um traço que influencia pensamentos, humor e decisões.

- **Facetas:** de 10 a 12 traços contínuos, de baixo a alto. Ansiedade, raiva, coragem, empatia, curiosidade, ambição, paciência, sociabilidade, ordem, sensibilidade à beleza, religiosidade, honestidade. Uma pessoa ansiosa sente mais os pensamentos ruins. Uma pessoa com muita raiva reage mais rápido a uma ofensa.
- **Valores:** o que a pessoa considera certo, com força própria: lei, família, tradição, poder, fé, lealdade, liberdade. Um valor forte gera pensamentos quando é respeitado ou quebrado. Exemplo: "alguém roubou da minha família" pesa muito numa pessoa para quem família é o valor principal.
- **Traços incomuns:** poucos traços discretos, como piromania, gulodice e ganância. Não substituem as facetas. Cada traço incomum ativa comportamentos específicos quando o contexto aparece: uma pessoa piromaníaca procura fogo e pode ateá-lo. Traços incomuns são raros e vêm por herança ou por experiência marcante.
- **Herança:** filhos herdam metade das facetas, dos valores e dos traços incomuns dos pais, com pequena mutação.
- **Mudança:** facetas e valores mudam devagar com a experiência. Um ousado que quase morreu pode virar cuidadoso.
- **Desejo:** cada pessoa tem um desejo (um abrigo próprio, filhos, vingar alguém). A estrutura vem do `Persona` copiado.

### 7.4 Necessidades e preferências

| Necessidade | Sobe quando | Satisfeita por |
|---|---|---|
| Fome | Passam as horas | Comer: caça, coleta, comida guardada |
| Sede | Passam as horas | Água |
| Sono | Muitas horas acordado | Dormir em abrigo (melhor) ou ao relento |
| Calor | Frio, chuva | Abrigo, fogo, roupa |
| Segurança | Predador, inimigo, perda | Abrigo, grupo, distância do perigo |
| Companhia | Isolamento | Convívio e afeto |
| Família | Afastamento de parentes | Estar perto de parentes |
| Sentido | Morte próxima, desamparo | Rituais, ocupação, vínculo, crença |
| Arte | Dias sem nada bonito ou sem criar | Fazer, ver ou ouvir algo bonito |
| Bebida | Dias sem bebida fermentada ou sem festa | Cerveja, hidromel, festas |

A urgência é uma curva convexa. Abaixo do limiar quase não pesa, acima domina. Isso gera decisões urgentes sem código especial.

**Preferências** são coisas de que a pessoa gosta ou não: comida, bebida, material, animal, lugar, ofício, outra pessoa. Gostar de algo gera pensamentos positivos quando aquilo está por perto ou é usado. Detestar gera o contrário. Preferências nascem da personalidade e da experiência, e também podem ser herdadas.

**Bebida fermentada** dá prazer e humor. Na v1 não cria dependência: é um prazer, não um vício.

### 7.5 Crenças, memória e relações

Cada pessoa mantém:

- **Lugares conhecidos:** tile, última vez visto, quantidade estimada e confiança. A confiança decai com o tempo.
- **Pessoas conhecidas:** onde foram vistas, estado (vivo, doente, zangado) e **relação**: afinidade de −1000 a 1000, amizade, amor, parentesco, rivalidade ou rancor. Rancor guarda a memória de uma ofensa específica.
- **Saberes:** receitas e práticas que a pessoa domina, com a origem de cada um e o grau de confiança.
- **Eventos marcantes:** os últimos acontecimentos relevantes, com peso emocional.
- **Obras e registros:** livros, tábuas e obras de arte que a pessoa leu ou viu viram memória, mesmo sem ter vivido o fato.

A memória tem capacidade limitada. O que não é reforçado esquece. Disso sai uma consequência central: **perder um saber é um evento**. Se a última pessoa que sabia acender fogo morre sem ensinar ninguém, o grupo esquece. A crônica registra isso. Mas se o saber estava escrito, outra pessoa pode reaprendê-lo: o registro sobrevive a quem o tinha.

### 7.6 Pensamentos e humor

- Cada pessoa tem uma lista de pensamentos recentes. Cada pensamento tem um peso, positivo ou negativo, e uma duração que diminui com o tempo. Exemplos: "comi um bom peixe" (+), "dormi num abrigo quente" (+), "vi um companheiro morrer" (−−, dura semanas), "alguém desrespeitou minha família" (−, longo se o valor é forte). O número de pensamentos ativos por pessoa é limitado, de 10 a 20.
- **Humor** é a soma dos pensamentos, mais as necessidades atendidas, menos as necessidades em falta. As facetas amplificam ou atenuam essa soma.
- Ver uma obra de arte ou ler um registro também gera pensamento. Um vizinho que adoeceu gera medo; quem cuidou dele pode sentir orgulho ou exaustão.
- O humor vira comportamento. Acima de um limiar, a pessoa trabalha melhor e procura companhia. Abaixo, evita gente e perde tempo. Nos extremos, aparecem as quebras da seção 7.10.
- O humor liga o mundo à pessoa. Uma morte próxima não é só um evento: muda o humor de todos que a conheciam, e cada um pensa nela de um jeito, conforme as facetas e os valores.

### 7.7 Ofício, habilidade, paixão e liberdade

- **Ofício preferido:** cada pessoa gosta de algumas atividades: caçar, colher, construir, cozinhar, fazer ferramenta, curar, ensinar, pintar, cantar. A preferência vem da personalidade e da experiência.
- **Habilidade:** cada atividade tem um nível que sobe com a prática e enferruja sem uso. Gosto e habilidade são coisas diferentes: uma pessoa pode gostar de caçar e ser ruim nisso.
- **Paixão:** cada habilidade tem um nível de paixão: nenhuma, pouca ou muita. A paixão multiplica o aprendizado e a satisfação de praticar. Quem tem muita paixão por cozinhar aprende mais rápido e fica mais feliz cozinhando, mesmo sem ser bom nisso ainda. A paixão nasce do gosto e pode crescer com a prática.
- **Escolha:** a pessoa decide o que fazer com base na necessidade mais urgente, no gosto, na habilidade e no humor. Ninguém manda nela. Se o grupo não tem caçador, a fome de todos pesa nas escolhas, e alguém acaba caçando, por necessidade e não por ordem.
- **Liberdade real:** pessoas vagam, visitam conhecidos, param para olhar um rio, têm impulsos (um desejo espontâneo de fazer algo bonito ou ir a um lugar). Impulsos vêm do humor e da personalidade, e entram na decisão como qualquer outro objetivo.
- **Profissão:** é o ofício em que a pessoa mais se destaca e mais gosta. Não é um cargo atribuído. Vira "profissão" quando a prática, a paixão e o gosto convergem, e pode mudar com a vida.

### 7.8 Decisão

Três passos:

1. **Utilidade** escolhe o *objetivo*: "comer", "ajudar Bento", "ir ao rio", "fazer uma faca bonita".
2. **Planejamento** monta a sequência para cumprir o objetivo, usando pré-condições e receitas. Exemplo: "fazer lança" exige pedra, madeira e lâmina. Se falta algo, o plano inclui buscar.
3. **Execução** roda a ação em ticks e é interrompida por evento.

Score ilustrativo. Não é a fórmula final:

```
Score(ação) = Σ urgência(n) · peso(faceta, n) · satisfaz(ação, n)
              + gosto(ação) + habilidade(ação) · peso + paixão(ação)
              − custo(distância, duração, risco)
              + termo_social(afinidade, valores, normas, pedidos)
              + impulso(humor, faceta)
              + inércia(ação atual)
```

A **inércia** é o bônus para continuar o que já se faz. Sem ela, as pessoas oscilam entre duas ações a cada tick. Esse é o bug típico de sistemas de utilidade, e o primeiro a ser testado.

Interrupções: predador ou inimigo na percepção, necessidade crítica, pedido de alguém próximo, morte de alguém próximo, pensamento forte, quebra mental, mudança brusca de clima.

### 7.9 Interações sociais

Interações são ações sociais com tipo. Cada pessoa escolhe a interação conforme humor, facetas e relação com a outra. O sucesso depende de sociabilidade e da relação entre as duas, e nunca é garantido:

| Interação | Quando acontece | Efeito |
|---|---|---|
| Conversa casual | Companhia baixa e alguém por perto | Relação sobe um pouco; humor sobe |
| Conversa profunda | Relação forte, tempo livre, sociabilidade alta | Relação sobe muito; pode trocar saberes ou segredos |
| Ensino | Habilidade alta, afinidade e ofício em comum | Transfere saber (seção 8) |
| Insulto | Raiva alta, rancor ou desentendimento | Relação cai; pode virar rancor |
| Cortejo | Afinidade alta, idade adequada e sociabilidade | Pode virar romance; rejeição pesa no humor |
| Briga | Insulto sem resposta e raiva alta | Ferimento possível; base para feud (seção 8) |

Uma falha pode piorar a relação. Sucesso e falha entram na memória das duas pessoas.

### 7.10 Quebras mentais e estados extremos

Quando o humor passa de um limite, a pessoa entra numa quebra mental. Como no RimWorld, as quebras têm três níveis:

- **Menores** (humor baixo por pouco tempo): vaga sem rumo, come demais, bebe demais, insulta alguém. Duram horas ou um dia.
- **Maiores** (humor muito baixo por dias): melancolia, com recusa de trabalho e de comida; fuga da região; catatonia breve. Duram dias ou semanas.
- **Extremas** (raiva ou desespero no limite): surto de raiva, ataque a quem estiver perto, quebra de objetos e incêndio. Duram minutos a horas e deixam marca na memória de quem viu.

As quebras surgem da combinação de humor, facetas e um gatilho: um insulto, uma perda, uma injustiça contra um valor forte. Quem fica por perto sente. Quando acontecem, aparecem na crônica.

Além das quebras, existe a **inspiração**, o estado criativo do Dwarf Fortress. Um artesão com habilidade alta e humor alto trabalha sem parar e pode produzir um artefato único (seção 6.7). Dura poucos dias.

Ninguém é programado para entrar nesses estados. A chance vem do humor, das facetas e do gatilho.

### 7.11 Catálogo de ações (v1)

| Grupo | Ações |
|---|---|
| Sobrevivência | Comer, beber, dormir, descansar, abrigar-se, acender fogo |
| Coleta | Colher frutas e raízes, pescar, juntar madeira, pegar pedra e argila |
| Caça | Rastrear, caçar, carregar a carcaça, esfolar, cozinhar |
| Produção | Fazer ferramenta, construir abrigo, trançar cesto, plantar, colher, cerâmica (fase 7), fazer prótese (fase 5) |
| Arte | Pintar, gravar, esculpir, cantar, fazer adorno, fazer artefato |
| Escrita | Escrever, ler, copiar um registro |
| Social | Conversar, dar comida, ensinar, pedir ajuda, cuidar de criança, cortejar, formar casal (interações: seção 7.9) |
| Cuidado | Cuidar de ferido, cuidar de doente, isolar um doente |
| Conflito | Discutir, brigar, fugir, cobrar dívida, vingar |
| Ritual | Enterrar, oferecer, marcar lugar sagrado (fase 6) |
| Exploração | Explorar, marcar caminho, avisar o grupo, visitar ruína |

### 7.12 Animais

Mente instintiva: fome, medo, reprodução e território. Sem memória social, sem normas, sem linguagem. Usam os dados copiados do `Bestiary` e o mesmo pathfinding. São entidades com IA, mas com um cérebro bem menor.

---

## 8. Da pessoa ao grupo

A sociedade não é um módulo. É o efeito de muitas mentes com memórias parecidas. Cada mecanismo abaixo tem uma **regra mínima**, que é o que o código faz, e um **efeito emergente**, que é o que o observador vê.

| Fenômeno | Regra mínima | Efeito emergente | Fase |
|---|---|---|---|
| Família | Casais, filhos herdam traços, cuidado de criança | Linhagens; herança de saber e de objetos | 4 |
| Vínculo | Afinidade sobe com convívio e ajuda, cai com ofensa | Amizades, rivais, pequenas facções | 3 |
| Bando | Agrupamento de pessoas com alta afinidade e moradia comum, detectado por dia | Grupos que se formam, se dividem e se fundem | 6 |
| Ensino | Ensinar transfere um saber, com chance ligada à afinidade e à habilidade | Ofício que se espalha; tradições locais | 5 |
| Imitação | Quem tem prestígio tem suas práticas copiadas | Modas, rituais, jeitos de fazer | 5 |
| Norma | Regra com escopo. Adotada quando a maioria pratica e os líderes apoiam. Reforçada ou punida por reputação | Divisão de comida, respeito à dormida, tabu | 6 |
| Propriedade | Uso repetido de um recurso gera *reivindicação*. Quebrá-la gera disputa | Campos, abrigos e árvores "de alguém" | 6 |
| Dívida | Livro de obrigações: quem deve a quem | Trocas, favores, cobrança | 6 |
| Liderança | Influência = prestígio (sucesso, idade, generosidade) + facetas. Decisões do grupo são ponderadas pela influência | "Quem todo mundo consulta". O nome do líder aparece na crônica, não como cargo | 6 |
| Assentamento | O grupo fica no mesmo lugar por anos e tem armazenamento | Acampamento vira aldeia | 7 |
| Divisão de trabalho | A necessidade do grupo puxa alguém para um ofício que falta | Caçador, ceramista, construtor | 7 |
| Feud | Ofensa guardada vira rancor persistente. Vingança vira objetivo | Vendetas que atravessam gerações | 8 |
| Cisão | Conflito + escassez + distância | O grupo se parte em dois | 8 |
| Crença | Pessoas buscam explicação para morte, fogo e tempestade. Explicações se espalham por imitação | Ritos de enterro, oferendas, mitos | 6 |
| Nomes | Pessoas nascem com nomes do grupo. Lugares ganham nome no primeiro evento marcante | Dialetos de nome que derivam com o tempo | 2 |
| Relação entre grupos | Contato leva a troca, casamento entre bandos ou disputa por recurso | Alianças, trocas, guerra (só com escassez e hostilidade) | 8 |
| Ideias culturais | Ideia com efeito (um gosto, um tabu, um rito). Espalha-se por imitação e convivência; pode ser abandonada | Costumes com razão própria, que mudam com o tempo | 6 |
| Escrita e registros | Fatos e saberes são gravados; quem lê aprende sem ter convivido com quem sabia | Saberes sobrevivem às mortes; disputas sobre quem disse o quê | 5 |
| Arte narrativa | Obra que retrata um fato. Quem vê guarda uma memória dele | Fatos ganham vida além de quem viu; a lenda vira objeto | 5 |
| Hierarquia de status | Cômodo bom e depósito bem cuidado dão prestígio a quem os tem | Diferença de status sem cargo; invejas e disputas por casa | 7 |
| Migração | Gente de fora chega ao vale e traz saber, facetas e rancor | Ideias novas e conflitos; grupos que se misturam | 8 |

Notas de desenho:

- **Nenhum cargo pré-definido.** O sistema não cria um chefe. Cria influência. O nome do papel aparece depois, na crônica, quando o padrão está estável.
- **Ninguém decide "fazer uma religião".** A crença nasce da tentativa de explicar perdas. O ritual se espalha porque quem o pratica é imitado. O mesmo vale para os mitos da história (seção 6.6).
- **Normas são observadas, não impostas.** A simulação não diz "roubar é proibido". Diz que roubar gera reputação negativa e que a maioria desaprova. Se o grupo passa a punir, a norma existe.
- **Registros e arte são memória coletiva.** Um fato escrito ou pintado sobrevive a quem o viveu. Isso dá peso às lendas e às perdas.

---

## 9. Tecnologia: de pedra a metal

A progressão é por conhecimento, não por script. Cada item aparece quando alguém o descobre por experimento ou aprende por ensino. Só se faz o que as receitas e os materiais permitem.

| Marco | Como surge | Pré-requisito | Fase |
|---|---|---|---|
| Ferramenta de pedra | Experimento de lascar pedra | Pedra | 5 |
| Fogo | Experimento com atrito ou centelha. Chance ligada à curiosidade e à isca | Madeira seca, pedra | 5 |
| Abrigo simples | Construção com galho e folha | Madeira, folha | 5 |
| Cesto e corda | Trançar fibras | Fibra vegetal | 5 |
| Lança e arco | Combinação de ferramentas | Ferramenta de pedra, madeira | 5 |
| Marcas de contagem | Riscos ou nós para dívidas e estoques | Qualquer | 5 |
| Escrita | Símbolos que registram fatos e saberes | Marcas de contagem, pedra ou argila | 5 |
| Arte figurativa | Pintura ou gravação de uma caça ou de uma batalha | Pigmento, pedra, tempo | 5 |
| Prótese | Membro de madeira ou metal feito por um fabricante | Madeira ou metal, ofício de fabricação | 5 |
| Livros e placas | Registros duráveis de contas, fatos e receitas | Escrita, pergaminho ou tábua | 6 |
| Cerâmica | Argila queimada no fogo | Argila, fogo | 7 |
| Armazenamento | Potes e cestos para guardar | Cerâmica ou cesto | 7 |
| Agricultura | Plantar semente, colher, guardar semente | Sementes, tempo | 7 |
| Barco | Canoa de tronco | Machado, fogo | 7 |
| Cobre e bronze | Forno e minério | Fogo intenso, minério | Opcional |

Ponto importante: as receitas de `Trades.Recipes` são de ofício medieval (mineiro que funde barras de cobre e ferro, ferreiro, escriba). A tecnologia pré-histórica acima é **dado novo**, e nasce dentro do Chronicle. As receitas copiadas servem de modelo de estrutura, não de conteúdo.

---

## 10. Lendas e crônica

Duas camadas de história, uma para o passado e outra para o presente:

- **Lendas:** a história procedural (seção 6.6). Fica fixa depois de gerada e é consultável no visualizador.
- **Crônica:** o registro da região viva, gerado em tempo real. Cada evento tem `{tick, tipo, atores[], lugar, dados, importância}`. Nada na crônica é inventado depois.

**Detector de marcos** (crônica ao vivo). Regras que olham o estado do mundo e registram a primeira vez que algo acontece:

- Primeiro fogo aceso.
- Primeira ferramenta feita.
- Primeiro abrigo de pé.
- Primeiro nascimento no vale.
- Primeira morte por violência.
- Primeiro enterro.
- Primeira reserva de comida guardada.
- Primeira norma observada.
- Primeiro conflito que virou feud.
- Primeira cisão do grupo.
- Primeiro lugar nomeado pelo grupo.
- Primeira colheita plantada.
- Primeiro assentamento permanente.
- Primeiro contato com outro grupo.
- Primeira troca.
- Primeiro artefato com nome.
- Primeira doença que atravessa o grupo.
- Primeiro registro escrito.
- Primeira obra que retrata um fato.
- Primeira chegada de estrangeiros.
- Primeira prótese.
- Primeira quebra mental extrema.
- Primeira inspiração que vira artefato.
- **Saber perdido:** o último que sabia algo morreu sem ensinar e sem deixar registro.

**Renderização:**

1. **Template bilíngue** com fragmentos EN e PT, pelo padrão de `Loc`. Obrigatório. Funciona sem internet. As frases de base vêm de `History.cs`, adaptadas ao tom da crônica.
2. **Polimento opcional por LLM** para tom e fluidez. O resultado é guardado no log, então reproduzir a história não chama o modelo de novo.
3. Se o LLM estiver indisponível, o template basta.

**Importância.** Cada entrada tem um peso. A crônica mostra as entradas acima do limiar. O resto fica no registro detalhado, filtrável.

**Nomes.** Os nomes de pessoas, povos, sítios e artefatos são gerados pelo mundo, a partir dos padrões de cada cultura. Eles **não são traduzidos**: são parte do mundo, como nomes próprios de verdade. Só o texto em volta é traduzido.

**Obituários.** Cada morte fecha uma biografia curta, montada a partir do log daquela pessoa. O `Morgue` copiado guarda partidas encerradas como dados simples: só o formato de registro vem dele. A ideia de obituário é nova.

---

## 11. Visualizador (somente leitura)

Layout denso, no estilo Dwarf Fortress, com a paleta Phosphor & Bone:

- **Mapa** no centro: terreno, pessoas (glifo com a cor do grupo), animais, abrigos, campos, fogueiras, ruínas e tumbas. Surtos de doença aparecem como áreas marcadas. A câmera pode seguir uma pessoa.
- **Barra de tempo:** ano, estação, dia e hora; velocidade; pausa.
- **Painel da pessoa** (clique): nome, idade, estágio, histórico de vida (origem e perdas), facetas e valores em linguagem simples, necessidades em barras, humor com os pensamentos mais fortes, ação atual **e o porquê** ("procura comida: fome 82%, rio a 9 tiles"), relações principais, ofício, habilidades e paixões, saberes.
- **Painel do grupo:** membros, comida guardada, local, ofícios que o grupo tem e os que faltam, normas vigentes, líder de influência, doentes e feridos.
- **Crônica:** rolagem com filtro (pessoas, grupo, cultura, natureza, quebras mentais).
- **Lendas** (tecla L): busca por figura, sítio, guerra, artefato, mito, registro ou obra. Cada página lista o que aconteceu e liga a outras páginas: quem casou com quem, quem matou quem, por quais mãos um artefato passou, qual obra retrata qual fato.
- **Gráficos:** população, comida, saúde do grupo, número de saberes, número de normas, humor médio.
- **Semente:** exibida e copiável. Tecla para gerar nova.

Controles, nenhum deles altera o mundo: Espaço pausa · 1–5 velocidade · F seguir · Tab próxima pessoa · Enter inspecionar · C crônica · L lendas · N nova semente.

O visualizador só lê frames. O shell não tem regra de jogo, como manda o `AGENTS.md` do Ossuary. Um teste garante que o hash de estado é idêntico com e sem visualizador e em qualquer velocidade.

---

## 12. Caminhos de IA

Este é o ponto que precisa da sua confirmação.

| Caminho | Como funciona | Prós | Contras |
|---|---|---|---|
| **A. Utilidade e planejamento em código** | Cada mente é código determinístico: score de utilidade, humor e planejamento por receitas | Roda com centenas de pessoas; reproduzível pela semente; testável em bot | Fala e nomes precisam de texto, resolvido na fase 6 |
| **B. Um LLM por pessoa** | Cada pessoa é consultada a um modelo para decidir | Decisões com cara de pensamento | Caro, lento, não reproduzível, não escala, impossível de testar em massa |
| **C. Híbrido: A + LLM como camada de linguagem** | A para decidir. LLM só para fala, mitos, nomes e polimento da crônica. Resultados gravados no log | Fala rica; o mundo continua reproduzível | Uma dependência a mais, opcional |

**Recomendação: A + C.** A mente é código. A linguagem pode ser rica. O LLM nunca escolhe uma ação.

O Dwarf Fortress decide por prioridades, necessidades e humor, não por linguagem. O caminho A é o que bate com a referência.

---

## 13. Desempenho

Alvos iniciais, a medir no spike:

| Métrica | Alvo inicial |
|---|---|
| Pessoas simultâneas | 100 na região viva. Teto de testes: 300 |
| Mapa histórico | ~128 × 128 tiles |
| Mapa vivo | ~96 × 96 tiles |
| História procedural | 500 anos em até 10 segundos, em máquina de desenvolvimento |
| Velocidade de simulação | ≥ 2.000 ticks por segundo com 100 pessoas em máquina de desenvolvimento (≈ 1 ano simulado a cada 4–5 s) |
| Memória | Estado de um século em poucos megabytes. Checkpoint anual |
| Crônica | Sem crescimento sem limite: o registro detalhado é compactado por ano |

---

## 14. Testes e validação

Sete camadas:

1. **Unitários:** Rng por subsistema, curvas de urgência, score de utilidade, humor e decaimento de pensamentos, contágio e imunidade, receitas, ferimentos, interações e seus sucessos.
2. **Invariantes, a cada tick em testes:** nenhuma pessoa em tile bloqueado; população = nascimentos − mortes; estoques ≥ 0; nenhum valor fora de faixa; toda pessoa viva tem posição; todo saber tem origem registrada.
3. **Determinismo:** mesma semente, mesmo hash, em 1× e na velocidade máxima, com e sem visualizador, e em outra máquina (CI).
4. **Regressão dos primitivos copiados:** para as mesmas sementes, `Rng`, `Fov` e `Pathfinder` produzem a mesma saída que antes de qualquer adaptação. Os valores são capturados do código copiado antes da primeira mudança e comparados a cada build.
5. **Consistência da história:** toda figura morta não age; todo artefato tem dono atual válido; toda ruína tem sítio de origem; toda lenda cita figuras e lugares que existem; todo registro escrito e toda obra de arte apontam para fato que existe na história. Mesma semente, mesmo catálogo de lendas.
6. **Soak de sementes:** 100 sementes × 300 anos, com relatório JSON. Segue o padrão de `headless.ps1 soak` e `balance` do Ossuary.
7. **Paridade bilíngue:** toda string tem PT e EN, como o teste de `Loc` do Ossuary.

**Métricas de emergência** acompanhadas no soak. São alvos para calibrar, não promessas:

| Métrica | Pergunta | Alvo inicial |
|---|---|---|
| Sobrevivência nos primeiros 20 anos | O sistema se extingue sozinho? | ≥ 80% das sementes |
| Tempo até o fogo | A descoberta acontece sem script? | Ocorre em ≥ 60% das sementes |
| Tempo até o primeiro assentamento | A sedentarização surge? | Em ≥ 40% das sementes, em 150 anos |
| Saberes perdidos | A perda de conhecimento acontece? | Ocorre, mas não em todas |
| Normas observadas | As normas surgem? | ≥ 1 por execução |
| Pessoas paradas ou oscilando | Há travamento? | Quase zero, com watchdog |
| Diversidade de ações | O mundo não colapsa em uma atividade? | Nenhuma ação passa de 60% do tempo |
| Figuras com vida rica no passado | A história tem gente com atos? | ≥ 50 figuras com pelo menos 3 atos cada, em 300 anos |
| Quebras mentais | Os estados extremos são raros? | Menores e maiores em menos de 5% das pessoas-ano; extremas em menos de 1% |
| Humor | O humor fica no meio da escala? | Humor médio entre 40% e 70% da maior parte do tempo |
| Surtos de doença | As doenças aparecem sem script e não varrem o grupo? | Surto em ≥ 50% das sementes em 50 anos; grupo sobrevive ao surto em ≥ 70% dos casos |
| Registros e obras | A escrita e a arte aparecem e são usadas? | ≥ 1 registro escrito em ≥ 60% das sementes, em 150 anos |

**Critério humano.** Antes de avançar de fase, assista a três execuções e leia duas ou três lendas. Escreva o que surpreendeu. Se nada surpreendeu, o problema não é de código, é de regra.

---

## 15. Fases

Cada fase fecha com teste automatizado, uma demo (ASCII, texto ou visualizador) e atualização da documentação. Não há prazo estimado aqui.

| Fase | Entrega | Pronta quando |
|---|---|---|
| **F0 Spike** | Base copiada (Rng, mapa, FOV, pathfinding); renderer copiado; região viva com terreno básico; 10 pessoas que andam, comem e morrem; dump ASCII; medida de ticks por segundo | Base compila sozinha; regressão dos primitivos passa; hash determinístico; desempenho registrado |
| **F1 Mundo** | Mundo histórico com geologia, biomas e rios; região viva recortada; clima e estações; fauna com ecologia (`Bestiary`); visualizador ASCII | Mesma semente, mesmo mundo; presas e predadores oscilam sem script |
| **F2 História** | Simulação anual de povos, figuras, sítios, guerras, mitos e artefatos; registros, inscrições e obras que sobram nas ruínas; lendas consultáveis em texto; nomes por cultura | Mesma semente, mesma história; ruínas aparecem na região viva; figuras têm vida coerente |
| **F3 Mentes** | Histórico de vida; facetas, valores e traços incomuns; necessidades e preferências; pensamentos e humor; relações; interações sociais; paixão, ofício e liberdade; decisão por utilidade; coleta | Pessoas sobrevivem um ano, escolhem ofícios de forma previsível pelo perfil e têm interações com tipos |
| **F4 Vida e corpo** | Idade, família, nascimento, morte; corpo, ferimentos e cuidado de ferido; doenças com contágio e imunidade; obituário (`Morgue`); túmulos | Gerações aparecem; cada morte tem causa, obituário e túmulo; uma doença atravessa o grupo sem script |
| **F5 Ofícios e artefatos** | Habilidades que enferrujam; receitas e fabricação (`Trades`, `Crafting`); próteses; escrita e registros; arte que retrata fatos; ensino e imitação; inspiração com artefato nomeado e histórico de donos | Artefatos e registros entram nas lendas; saber registrado sobrevive a quem o tinha |
| **F6 Grupo e crônica** | Bandos, normas, propriedade, dívida, liderança, crenças e ritos; ideias culturais; boatos, registro de atos e crônica bilíngue; quebras mentais em três níveis; pressões do mundo | Bandos se formam e se dividem; ≥ 1 norma observada; quebras aparecem sem travar; crônica lê como história |
| **F7 Assentamento e economia** | Armazenamento; zonas e cômodos com valor; agricultura; cerâmica; aldeia; divisão de trabalho; hierarquia de status; mercado local, regateio e caravanas | Aldeia aparece em parte das sementes |
| **F8 Relações entre grupos** | Migrantes e refugiados; saques, cisão, feud, troca, guerra entre bandos; facções | Duas bandas interagem sem script; uma migração muda o grupo |
| **F9 Visualizador completo** | Renderer e CRT copiados; painéis; lendas navegáveis; gráficos; sons opcionais; semente compartilhável; LLM opcional para polimento | Quem assiste segue uma pessoa e navega lendas sem ajuda |
| **F10 Balanceamento** | Soak de 100 sementes, métricas de emergência, ajuste de números | Métricas nos alvos da seção 14 |
| **Opcional** | Metal, domesticação, magia, criaturas lendárias, camadas subterrâneas, fluidos, mais de um mundo | Decidir depois do F10 e das perguntas da seção 18 |

---

## 16. Riscos

| Risco | Probabilidade | Mitigação |
|---|---|---|
| Escopo: o Dwarf Fortress levou décadas e a referência é enorme | Alta | Núcleo de cada área na v1 (seção 3.1); resto em Opcional; "pronta quando" em cada fase |
| Muitos sistemas novos de uma vez (doenças, quebras, interações, escrita, pressões) | Alta | Uma família de sistemas por fase; cada uma testada isolada antes de juntar |
| Nada interessante emerge: mundo morto ou caótico | Alta | Métricas de emergência; soak de sementes; botões de recurso; começar generoso e apertar aos poucos |
| História repetitiva: povos e guerras parecidos entre sementes | Média | Padrões de cultura por povo; teste de diversidade por semente; regras variadas para guerra e fundação |
| Pessoas travadas ou oscilando entre ações | Média | Inércia; histerese; watchdog de ação; invariantes em teste |
| Pensamentos demais tornam o sistema lento ou ilegível | Média | Limite de 10 a 20 pensamentos ativos por pessoa; decaimento; só o forte aparece na tela |
| Doenças e quebras mal calibradas acabam com o grupo | Média | Métricas de sobrevivência e de quebra no soak; ajuste de números na F10 |
| Pressões do mundo se somam e viram azar constante | Média | Limite de pressões ao mesmo tempo; chance sobe só com condição somada (seção 6.8) |
| Lentidão com muitas pessoas | Média | Ciclo por evento; orçamento por tick; fila de pathfinding; hash espacial |
| Quebra do determinismo (ponto flutuante, ordem de dicionário, `Rng` global, LLM) | Média | Auditoria do código copiado (5.4); inteiros; ordem por id; LLM gravado no log; hash dourado no CI |
| Crônica ou lendas viram ruído | Média | Importância por entrada; limiar; registro detalhado separado |
| Adaptar demais: tirar `Game` e `Player` de um arquivo custa mais do que escrever do zero | Média | Começar pelos sistemas menos acoplados; medir o esforço por sistema; reescrever quando passar do esperado (5.1.1) |
| Custo ou latência do LLM | Baixa, se opcional | Opcional; orçamento por dia simulado; cache; template como padrão |

---

## 17. Decisões assumidas neste rascunho

Você ainda não respondeu às perguntas da seção 18. Assumi o caminho mais provável. Todas são fáceis de trocar:

1. **Dwarf Fortress é a referência principal.** Na dúvida de design, vale o que o DF faria, salvo conflito com um princípio deste documento.
2. **RimWorld é a segunda referência,** para a vida interna das pessoas: quebras, interações, passados, traços e paixões. O DF manda na história e no mundo.
3. **Mecânicas e ideias, não código nem texto.** O código e os textos vêm do Ossuary ou são escritos do zero.
4. **Projeto isolado:** `C:\dev\chronicle`. Nenhum build aponta para `C:\dev\ossuary`.
5. **Reuso por cópia e adaptação,** sem sincronização com o Ossuary.
6. **Uma biblioteca só,** `src/Chronicle/`, organizada por sistema.
7. **Namespace próprio** (`Chronicle`). Os arquivos copiados mantêm o aviso de copyright do Ossuary.
8. **História procedural antes da chegada:** 300 a 500 anos, em passos anuais, no mundo histórico.
9. **Dois níveis de simulação:** figuras históricas com modelo anual simples; pessoas vivas com mente completa, em horas.
10. **Duas escalas de mundo:** mundo histórico de ~128 × 128 e região viva de ~96 × 96.
11. **Lendas consultáveis no visualizador,** já na v1.
12. **Motor de história em simulação de atos,** como no DF. Templates ficam só para texto.
13. **Pressões do mundo por regra e sorteio,** sem diretor de eventos.
14. **Quebras mentais em três níveis:** menores, maiores e extremas.
15. **Bebida fermentada como prazer,** sem dependência na v1.
16. **Próteses na fase 5,** porque dependem de fabricação.
17. **IA:** caminho A + C. Mente em código, LLM opcional só para linguagem.
18. **Escala:** grupo fundador de 8 pessoas; teto de testes de 300.
19. **Tempo:** 1 tick = 1 hora na região viva; ano de 360 dias.
20. **Fora da v1:** magia, raças fantásticas, criaturas lendárias e subterrâneo.
21. **Sem intervenção do observador.**
22. **Idioma:** este documento está em português. A crônica, as lendas e a interface são EN primeiro, com PT ao lado.
23. **Git.** O projeto está em `github.com/Bruno-BRG/chronicles`. Nenhum código do Ossuary entra antes da aprovação do plano da F0.
24. **Nenhum código copiado ainda.** A cópia começa no F0, depois da aprovação deste documento.

---

## 18. Perguntas em aberto

As primeiras são as que mais mudam o plano:

1. **IA por pessoa:** mentes em código com linguagem opcional por LLM (recomendado), ou um LLM de verdade por pessoa?
2. **Subterrâneo:** as camadas de minas e cavernas, como no DF, entram na v1 ou ficam para depois? Padrão: depois.
3. **Criaturas lendárias:** megafauna e bestas esquecidas, como no DF, entram como lendas do mundo histórico? Não são magia, mas são fantasia. Padrão: fora da v1.
4. **Universo:** mesmo universo do Ossuary, como um prólogo sombrio com os mesmos deuses e fauna, ou um mundo neutro? Padrão: neutro, sem magia.
5. **Passado:** quantos anos de história antes da chegada e quantos povos? Padrão: 300 a 500 anos, 2 a 4 povos.
6. **Escala:** 8 pessoas no início está bom? Qual o teto desejado, 100 ou 300?
7. **Colapso:** a civilização pode acabar de vez, ou deve ser sempre "vivível" por padrão? Padrão: pode acabar.
8. **Animais:** contam como IA? Padrão: sim, com mente instintiva.
9. **Metal e magia:** entram na v1 ou depois? Padrão: depois.
10. **Sincronização:** confirma que o código copiado é de partida, sem sincronização com o Ossuary? Padrão: sim.
11. **Idioma:** documento e crônica em português primeiro, ou inglês primeiro? Padrão: este documento em português; crônica e textos do jogo em EN primeiro, com PT ao lado.
12. **Som:** o observador ouve música e sinais de evento (`audio.ts`, `stingers.ts`)? Padrão: opcional, na fase 9.

---

## 19. Próximos passos

1. Você revisa este documento e responde às perguntas da seção 18, ou diz que está aprovado como está.
2. Com a aprovação, o próximo passo é o **plano de implementação** da fase F0 (o spike). Ele começa copiando a base (Rng, mapa, FOV, pathfinding) e o renderer com o CRT. Só depois disso começa código.
3. Até lá, nada é copiado nem implementado.

---

## Apêndice A — Glossário

- **Entidade:** qualquer ser com mente: pessoa ou animal.
- **Mente:** o conjunto de necessidades, memória, facetas, valores, pensamentos e planos de uma entidade.
- **Faceta:** traço contínuo de personalidade, como ansiedade ou curiosidade.
- **Valor:** o que uma pessoa considera certo, com força própria, como família ou lei.
- **Traço incomum:** traço raro e discreto, como piromania, que dispara comportamentos específicos.
- **Histórico de vida:** o passado de uma pessoa antes do presente: origem, ofício anterior, perdas e marcas.
- **Pensamento:** lembrança ou sensação com peso e duração, que compõe o humor.
- **Humor:** soma dos pensamentos e das necessidades, ajustada pelas facetas.
- **Ofício:** atividade que a pessoa pratica, com gosto e habilidade próprios.
- **Paixão:** nível de entusiasmo por uma habilidade (nenhuma, pouca ou muita).
- **Profissão:** o ofício em que gosto, paixão e habilidade convergem.
- **Interação social:** ação social com tipo, como conversa profunda, insulto ou cortejo.
- **Quebra mental:** colapso de humor em três níveis: menor, maior ou extremo.
- **Inspiração:** estado criativo intenso, que pode gerar um artefato.
- **Doença:** condição com estágios, contágio e imunidade.
- **Surto:** espalhamento de uma doença por um grupo, povo ou região.
- **Prótese:** membro de madeira ou metal que substitui um membro perdido.
- **Figura histórica:** pessoa notável do passado, com vida anual simplificada.
- **Povo:** civilização do mundo histórico, com território, valores e padrão de nomes.
- **Sítio:** vila, fortaleza, templo ou cemitério. Pode virar ruína.
- **Lenda:** página consultável de uma figura, sítio, guerra, artefato, mito, registro ou obra.
- **Artefato:** objeto único com nome, autor e histórico de donos.
- **Registro:** texto ou marca que guarda fatos ou saberes, e sobrevive a quem os viveu.
- **Obra de arte:** pintura, gravação ou escultura que retrata um fato.
- **Pressão do mundo:** condição que empurra a vida do grupo (seca, praga, guerra, migração), sorteada sem diretor.
- **Zona:** área de armazenamento com função.
- **Cômodo:** espaço com função e valor, que influencia o status de quem o usa.
- **Migrante:** pessoa de fora que chega ao vale.
- **Mundo histórico:** mapa grande onde a história procedural acontece.
- **Região viva:** recorte do mundo onde o grupo fundador vive, em horas.
- **Bando:** grupo detectado por afinidade e moradia comum. Não é um cargo.
- **Norma:** regra observada que um grupo pratica e reforça.
- **Reivindicação:** uso repetido de um recurso que o grupo passa a reconhecer como de alguém.
- **Marco:** evento detectado no estado do mundo, como o primeiro fogo.
- **Crônica:** registro em tempo real da região viva.
- **Saber:** receita ou prática que uma pessoa domina, com a origem registrada.
- **Código copiado:** trecho do Ossuary trazido por Ctrl-C, Ctrl-V e adaptado, registrado em `THIRD_PARTY.md`.
