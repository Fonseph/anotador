# ♟️ Anotador de Xadrez

Aplicativo web que usa a câmera do celular para **reconhecer e anotar automaticamente os lances** de uma partida de xadrez em tabuleiro físico. Roda inteiro no navegador (testado como alvo: Safari no iPhone), sem instalar nada e sem enviar imagens para servidor.

**Abrir o app:** https://fonseph.github.io/anotador/anotador-xadrez.html

## Como funciona

1. **Calibração:** com o vídeo ao vivo, toque nos quatro cantos do tabuleiro na ordem **a1 → a8 → h8 → h1**. O app endireita a imagem (transformação de perspectiva) e desenha a grade 8×8 por cima para você conferir.
2. **Posição inicial:** com as peças na posição inicial e as mãos fora do tabuleiro, o app guarda a imagem de referência.
3. **Detecção contínua:** o app compara, o tempo todo, a imagem atual com a última posição confirmada e mede a mudança em cada uma das 64 casas.
4. **Validação:** a mudança só vira lance se corresponder a um **lance legal** para quem joga (inclui roque e en passant, usando a biblioteca chess.js).
5. **Confirmação:** o mesmo lance precisa ser detectado de forma **consistente por cerca de 1 segundo**. A mão passando sobre o tabuleiro não gera lance.
6. **Lance inválido:** o app mostra o motivo (peça levantada, casa inválida, outra peça movimentada, peça devolvida) e espera a correção.

## Como usar

1. Abra o link no **Safari** e permita o acesso à câmera.
2. Preencha nome e cidade de cada jogador e toque em **Iniciar**.
3. Calibre os quatro cantos e confirme.
4. Jogue. Os lances aparecem na lista, com o tempo gasto em cada um.
5. Ao terminar, toque em **Finalizar**.

Dica: use **Compartilhar → Adicionar à Tela de Início** para ter um ícone de app. A calibração fica salva no aparelho; se o celular não mudou de lugar, use **Usar calibração salva**.

### Botões durante a partida

| Botão | O que faz |
|---|---|
| Desfazer | Remove o último lance (reponha as peças e aguarde) |
| Corrigir | Digita o lance correto, por exemplo `Nf3`, `exd5`, `O-O` |
| Recalibrar | Refaz a calibração dos cantos |
| Finalizar | Gera a súmula e os lances em texto |

## Exportação

Ao finalizar, o app gera:

- **Lances em uma linha**, pronta para copiar:
  `1. e4 e5 2. Qh5 Nc6 3. Bc4 Nf6 4. Qxf7# 1-0`
- **Súmula em PNG** com jogadores, cidades, data, resultado, lances e a posição final (segure a imagem para salvar em Fotos, ou use Compartilhar).
- **PGN** com cabeçalho, copiado para a área de transferência.

O resultado (`1-0`, `0-1`, `1/2-1/2`, `*`) é sugerido automaticamente quando a partida termina em mate ou empate e pode ser alterado.

## Posição da câmera

- O melhor é o celular **bem acima do tabuleiro, apontando reto para baixo (90°)**, centralizado.
- Se não for possível, fique a pelo menos **60° a 70°** da mesa, no meio de um dos lados. Abaixo de 45° o reconhecimento piora.
- O tabuleiro deve ocupar cerca de 80% a 90% da imagem, com os quatro cantos visíveis.
- Use a câmera **1x** (não a ultra-angular), luz uniforme, sem sombras nem reflexos.
- O celular precisa ficar **fixo** depois de calibrar (tripé ou suporte).

## Limitações conhecidas

- A promoção de peão é registrada como **dama**; para outra peça, use **Corrigir**.
- Peças altas vistas de lado podem "invadir" a casa vizinha na imagem, por isso a câmera de cima é melhor.
- O reconhecimento depende de boa luz e de câmera parada; pode ser necessário ajustar a sensibilidade em tabuleiros com pouco contraste entre peças e casas.
- A câmera ao vivo só funciona em página **HTTPS** (como o GitHub Pages); abrir o arquivo `.html` direto no celular não libera a câmera.

## Privacidade

Todo o processamento acontece no navegador do seu aparelho. As imagens da câmera **não são enviadas** a nenhum servidor. Nomes, cidades e a calibração ficam salvos apenas no armazenamento local do navegador. O repositório contém apenas o código do aplicativo.

## Tecnologias

- HTML, CSS e JavaScript (canvas para a retificação e comparação das imagens)
- [chess.js](https://github.com/jhlywa/chess.js) para as regras do xadrez e a validação dos lances
- GitHub Pages para hospedagem

## Atualizar o app no GitHub

1. No repositório, toque em **Add file → Upload files**.
2. Envie o novo `anotador-xadrez.html` com o **mesmo nome**.
3. Toque em **Commit changes** e espere cerca de 2 minutos.

## Próximos passos

- Ajuste fino da sensibilidade com testes em partidas reais
- Relógio de xadrez com tempo total de cada jogador
- Escolha da peça na promoção
