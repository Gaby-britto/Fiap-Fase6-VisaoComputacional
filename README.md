# FarmTech Solutions | Fase 6: Visão Computacional

**Grupo 35** | FIAP, Curso de Inteligência Artificial

Reconhecimento de dois objetos (**teclado** e **garrafa**) com três abordagens de visão computacional: YOLO customizada, YOLO tradicional e CNN treinada do zero.

## Integrantes

| Nome | RM | Responsável por |
|---|---|---|
| Gabriele Brito Rocha Menezes | rm574145 | Entrega 1: YOLO customizada |
| Gilenisson Lucas Bezerra dos Santos| rm573716 | Entrega 2: comparação de modelos |

## Links

| Item | Link |
|---|---|
| Notebook da Entrega 1 | [abrir](COLE_AQUI_O_LINK_DO_NOTEBOOK_1) |
| Notebook da Entrega 2 | [abrir](COLE_AQUI_O_LINK_DO_NOTEBOOK_2) |
| Vídeo de demonstração (YouTube, não listado) | [assistir](COLE_AQUI_O_LINK_DO_VIDEO) |

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

| Métrica | 30 épocas | 60 épocas |
|---|---|---|
| mAP50, melhor época (`best.pt`) | 0,758 | 0,970 |
| mAP50, última época | 0,812 | 0,809 |
| Recall, melhor época | 0,750 | 0,946 |
| Recall, última época | 0,749 | 0,864 |

Os dois treinos terminaram praticamente empatados em mAP50. No treino de 60 épocas, a loss de validação parou de cair e voltou a subir enquanto a de treino seguiu caindo, o que indica início de overfitting. A validação tem poucas imagens, então as métricas oscilam bastante. A análise completa, os prints das detecções nas imagens de teste e as limitações estão no notebook.

---

## Entrega 2: comparação de modelos

*Responsável: Gilenisson Lucas Bezerra dos Santos*

> Seção a ser preenchida pela Pessoa 2: abordagens comparadas (YOLO customizada, YOLO tradicional e CNN do zero), critérios (facilidade de uso, precisão, tempo de treino e tempo de inferência) e resumo da conclusão.

---

## Estrutura do repositório

```
.
├── README.md
├── NOME_rmXXXXX_pbl_fase6.ipynb      # Entrega 1
├── NOME2_rmXXXXX_pbl_fase6.ipynb     # Entrega 2
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
