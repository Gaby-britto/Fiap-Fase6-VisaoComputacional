# FarmTech Solutions | Fase 6: Visão Computacional

**Grupo 35** | FIAP, Curso de Inteligência Artificial

Reconhecimento de dois objetos (**teclado** e **garrafa**) com três abordagens de visão computacional: YOLO customizada, YOLO tradicional e CNN treinada do zero.

## Integrantes

| Nome | RM | Responsável por |
|---|---|---|
| Gabriele Brito Rocha Menezes | rm574145 | Entrega 1: YOLO customizada |
| Gilenisson Lucas Bezerra dos Santos | rm573716 | Entrega 2: comparação de modelos |

## Links

| Item | Link |
|---|---|
| Notebook da Entrega 1 | [abrir](GabrieleBritoRochaMenezes_rm574145_pbl_fase6.ipynb) |
| Notebook da Entrega 2 | [abrir](https://github.com/Gaby-britto/Fiap-Fase6-VisaoComputacional/blob/main/GilenissonLucasBezerzaDosSantos_RM573716_pbl_fase6%20.ipynb) | |
| Vídeo de demonstração (YouTube, não listado) | LINK A SER ADICIONADO |

Todo o passo a passo, o código executado e as análises completas estão nos notebooks. Este README apresenta o projeto e orienta a leitura.

## Contexto

A FarmTech Solutions está expandindo seus serviços de IA para além do agronegócio, incluindo visão computacional. Neste projeto, simulamos uma demonstração para um cliente que quer entender, na prática, o potencial e a acurácia de um sistema de detecção de objetos.

## Base de imagens

- **80 imagens**: 40 de teclado e 40 de garrafa.
- Divisão por classe: **32 treino, 4 validação e 4 teste** (total: 64 / 8 / 8).
- Rotulação feita no [Make Sense](https://www.makesense.ai/), exportada em formato YOLO.
- Classes: `0 = teclado`, `1 = garrafa`.

---

## Entrega 1: YOLO customizada

*Responsável: Gabriele Brito Rocha Menezes*

Treinamos o modelo **YOLOv8n** (Ultralytics), partindo dos pesos pré-treinados, para reconhecer as duas classes. Foram feitos dois experimentos com as mesmas configurações (`imgsz=640`, `batch=8`, `seed=42`), mudando apenas o número de épocas: **30** e **60**.

### Resultado resumido (validação, 8 imagens)

| Métrica (`best.pt`) | 30 épocas | 60 épocas |
|---|---|---|
| mAP50 | 0,995 | 0,912 |
| Recall | 0,981 | 0,750 |
| Precisão | 0,910 | 0,969 |
| Tempo de treino | 1,2 min | 1,6 min |

Mais épocas não trouxeram ganho claro: na validação, 30 épocas foram melhores, e no teste o modelo de 60 épocas acertou uma imagem a mais (7 de 8 contra 6 de 8), porém com caixas extras. O treino de 60 épocas mostrou sinal leve de overfitting. Como a validação tem poucas imagens, as métricas oscilam bastante. A análise completa, os prints das detecções nas imagens de teste e as limitações estão no notebook.

---

## Entrega 2: Comparação entre CNN, YOLOv5 tradicional e YOLO personalizada

*Responsável: Gilenisson Lucas Bezerra dos Santos*

Nesta etapa, foi desenvolvida uma CNN (*Convolutional Neural Network*) treinada do zero para classificar imagens de garrafas e teclados. O modelo foi avaliado utilizando um conjunto de teste com 8 imagens e obteve **87,5% de acurácia**, classificando corretamente 7 das 8 imagens.

Também foi avaliado o YOLOv5 tradicional, utilizando pesos pré-treinados. Nos testes realizados com as mesmas categorias de objetos, a classe esperada foi detectada em 2 das 8 imagens. O tempo médio de inferência observado foi de aproximadamente **1,0159 segundo por imagem**.

A YOLO personalizada desenvolvida na Entrega 1 foi treinada com imagens e anotações específicas para as classes de garrafas e teclados. Seus resultados devem ser analisados em conjunto com as métricas registradas no notebook correspondente.

**Conclusão:** os experimentos permitem comparar abordagens distintas de visão computacional. A CNN apresentou bom desempenho de classificação no pequeno conjunto de teste utilizado, enquanto o YOLOv5 tradicional apresentou limitações na detecção das classes esperadas. A comparação deve considerar que os modelos possuem objetivos diferentes: a CNN classifica a imagem, enquanto os modelos YOLO localizam e identificam objetos. O tamanho reduzido do conjunto de teste limita a generalização dessas conclusões.
---

## Estrutura do repositório

```
.
├── README.md
├── GabrieleBritoRochaMenezes_rm574145_pbl_fase6.ipynb   # Entrega 1
├── (notebook da Entrega 2)
├── dataset/
│   ├── data.yaml
│   ├── images/   (train, val, test)
│   └── labels/   (train, val)
└── resultados/
    ├── treino_30ep/   (results.csv, curvas, best.pt)
    ├── treino_60ep/   (results.csv, curvas, best.pt)
    └── testes/        (imagens processadas pelo modelo)
```

## Como executar

1. Abra o notebook desejado no Google Colab.
2. Ative a GPU: *Ambiente de execução → Alterar tipo → T4 GPU*.
3. Execute as células em ordem. O notebook clona este repositório para acessar o dataset, então não depende de nenhum Drive pessoal.

## Tecnologias

Python, Google Colab, Ultralytics YOLOv8, PyTorch, Make Sense.
