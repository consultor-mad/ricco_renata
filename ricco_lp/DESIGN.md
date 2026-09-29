# Design - Caixa Lucrativo Essencial

## Objetivo

Esta landing page apresenta o produto Caixa Lucrativo Essencial para MEIs e microempresas que precisam de clareza financeira recorrente. A experiencia deve ser direta, comercial e orientada a conversao, com uma narrativa simples: dor financeira, consequencia, solucao, funcionamento, qualificacao e chamada final.

## Estrutura da pagina

A pagina e um `index.html` estatico com CSS e JavaScript embutidos.

Ordem das secoes:

1. `lead-modal`: pop-up inicial de captura de lead.
2. `hero`: promessa central e CTA para diagnostico.
3. `checklist`: sintomas do problema financeiro.
4. `callout` e `graph-section`: reforco visual do risco de operar sem clareza.
5. `intro-section`: apresentacao do Caixa Lucrativo Essencial.
6. `list-section`: como funciona na pratica.
7. `response-section`: mini diagnostico interativo com botoes SIM/NAO.
8. `offer-section`: qualificacao do publico ideal e preco.
9. `dark-section`: chamada final para acao.

## Direcao visual

O design combina uma estetica de produto financeiro acessivel com elementos mais energicos de tecnologia.

- Base clara com secoes brancas e cinza claro.
- Roxo/azul como cor principal de marca e profundidade.
- Ciano/azul claro como cor de acao, destaque e progresso.
- Tipografia grande e assertiva para titulares.
- Cards simples e poucos elementos decorativos, priorizando leitura e conversao.
- Imagens em `assets/` funcionam como reforco visual da narrativa, nao como decoracao solta.

## Tipografia

Fontes importadas no topo do CSS:

- `League Spartan`: usada em titulos, CTAs grandes e textos de impacto.
- `Montserrat`: usada em corpo, labels, textos auxiliares e formularios.
- `Gobold`: usada em alguns titulos de maior impacto e chamadas em caixa alta.

Regra pratica:

- Use `League Spartan` para mensagens comerciais fortes.
- Use `Montserrat` para leitura e interface.
- Use `Gobold` apenas quando a secao precisa de mais peso visual.

## Paleta

Cores principais encontradas no CSS:

- Roxo principal: `#7976f2`
- Roxo escuro de estado/apoio: `#3d57f6`
- Ciano de acao: `#3ec7ee`
- Gradiente CTA: `#4dd2dd`, `#56c1e2`, `#59a1e2`, `#5b85e2`, `#6063e2`, `#6258e2`
- Texto escuro: `#0f1222`
- Fundo cinza: `#f2f2f2`
- Divisor: `#d9d9d9`
- Positivo: `#27c840`
- Negativo: `#ff5757`

Evite transformar a pagina em uma interface de uma cor so. O roxo deve ser dominante nas areas de impacto, enquanto branco, cinza e ciano equilibram leitura e conversao.

## Componentes

### Pop-up de lead

Classes principais:

- `.lead-modal`
- `.lead-form`
- `.lead-field`
- `.lead-submit`
- `.lead-feedback`

Campos atuais:

- Nome
- Email
- WhatsApp
- Empresa
- Margem de faturamento

Opcoes de faturamento:

- Ate 30 mil
- De 30 mil a 150 mil
- De 150 mil a 500 mil
- Mais que 500 mil

O formulario envia os dados via `fetch` para a constante `GOOGLE_SCRIPT_URL`, que aponta para um Web App do Google Apps Script. A planilha espera as colunas:

```txt
Data | Nome | Email | WhatsApp | Empresa | Origem | Margem de faturamento
```

Ao alterar campos no formulario, tambem atualize o Apps Script e os cabecalhos da planilha.

### CTAs

Classes principais:

- `.btn`
- `.offer-cta`
- `.dark-btn`
- `.lead-submit`

Os CTAs usam formato arredondado e cores de alto contraste. O CTA principal usa gradiente azul/ciano/roxo. Mantenha esse padrao para acoes primarias.

### Diagnostico SIM/NAO

Classes principais:

- `.response-section`
- `.response-list`
- `.response-btn`

Cada botao alterna entre `data-state="sim"` e `data-state="nao"`. O estado visual depende do atributo `data-state`, entao qualquer alteracao no JavaScript deve preservar esse contrato.

### Cards de oferta

Classes principais:

- `.offer-grid`
- `.offer-card`
- `.offer-card--green`
- `.offer-card--red`

Os cards separam claramente publico recomendado e publico nao recomendado. Preserve o contraste verde/vermelho para facilitar a leitura rapida.

## Assets

Os arquivos visuais ficam em `assets/`.

Principais usos:

- `background1.webp`: fundo/apoio visual de topo quando usado no layout.
- `hero-problema.webp`: imagem lateral da secao de checklist.
- `graph.webp`: grafico ilustrativo.
- `rico.webp`: icone/personagem da apresentacao.
- `tecnlogia.webp`, `logo-ia.webp`, `especialista.webp`: cards de pilares.
- `number1.webp` a `number6.webp`: passos da jornada.
- `check.webp` e `cross.webp`: qualificacao positiva/negativa.
- `arrow1.webp`: bullets da dor.

Antes de trocar um asset, confira se o novo arquivo tem proporcao parecida. Muitas imagens foram posicionadas por `background-size` ou largura fixa, entao proporcoes muito diferentes podem quebrar a composicao.

## Responsividade

Breakpoints existentes:

- `720px`: ajusta hero e checklist para telas menores.
- `540px`: ajusta o pop-up de lead.

Ao alterar textos, teste principalmente:

- Titulos grandes no mobile.
- Botao de preco `.offer-cta`.
- Campos do pop-up.
- Lista de perguntas da secao `response-section`.

## Integracao Google Sheets

O front envia um JSON para o Apps Script usando:

```js
fetch(GOOGLE_SCRIPT_URL, {
  method: 'POST',
  mode: 'no-cors',
  headers: {
    'Content-Type': 'text/plain;charset=utf-8'
  },
  body: JSON.stringify(payload)
});
```

Como `mode: 'no-cors'` nao permite ler a resposta detalhada no navegador, a validacao final deve ser feita conferindo se a linha apareceu na planilha ou no painel de execucoes do Apps Script.

Se a URL ou a aba mudar:

1. Atualize `GOOGLE_SCRIPT_URL` no `index.html`.
2. Atualize `SHEET_NAME` no Apps Script.
3. Salve o Apps Script.
4. Implante uma nova versao.
5. Teste enviando um lead real.

## Regras de manutencao

- Mantenha a pagina como experiencia direta, sem criar uma landing secundaria antes do conteudo.
- Evite adicionar muitos cards ou blocos explicativos longos.
- Nao remova o pop-up sem substituir por outro mecanismo de captura.
- Preserve o fluxo narrativo: dor, consequencia, solucao, funcionamento, qualificacao, acao.
- Ao adicionar novos campos de lead, mantenha nomes simples no atributo `name`, pois eles viram chaves no payload enviado ao Apps Script.
- Depois de qualquer mudanca no formulario, faca um teste real ate a planilha.
