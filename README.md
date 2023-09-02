# Conversor de Espaços de Cores e Analisador de Histogramas

Este é um aplicativo de desktop construído com a biblioteca PyQt5 e OpenCV que permite aos usuários selecionar uma imagem e converter sua representação de cores em diferentes espaços de cores. Além disso, ele oferece a capacidade de visualizar e salvar os histogramas das imagens resultantes.

## Funcionalidades

- **Selecionar Imagem**: O aplicativo permite que os usuários escolham uma imagem da sua galeria.

- **Conversões de Espaço de Cores**: O aplicativo oferece sete botões diferentes para converter a imagem original RGB em outros espaços de cores, incluindo Grayscale (escala de cinza), XYZ, YCrCb, HSV, HLS, CIE L*a*b*, e CIE L*u*v*.

- **Visualização de Histogramas**: Os histogramas das imagens resultantes podem ser visualizados em gráficos, mostrando a distribuição de intensidades de pixel para cada canal de cor. Isso ajuda na análise da distribuição de cores na imagem.

- **Salvar Imagens e Histogramas**: O aplicativo permite que os usuários salvem as imagens processadas e os histogramas em arquivos separados.

## Como Usar

1. Execute o aplicativo.
2. Clique no botão "Selecionar Imagem" e escolha uma imagem da sua galeria.
3. Após selecionar uma imagem, os botões para as conversões de espaço de cores ficarão habilitados.
4. Clique no botão correspondente à conversão que deseja realizar.
5. A imagem resultante será exibida em uma nova janela, juntamente com os histogramas (se aplicável).

## Pré-requisitos

- Python 3.x
- PyQt5
- OpenCV (cv2)
- Matplotlib

Você pode instalar as dependências usando o pip:

```bash
pip install PyQt5 opencv-python matplotlib
```

## Executando o Aplicativo

Para executar o aplicativo, basta executar o código Python fornecido. O aplicativo abrirá uma janela de interface do usuário.

```bash
python nome_do_aplicativo.py
```
---
