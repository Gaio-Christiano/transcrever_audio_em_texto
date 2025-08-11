# Transcrição de Áudio com Identificação de Locutores

Este projeto oferece um script Python para transcrever arquivos de áudio no formato MP3, gerando uma transcrição detalhada em arquivos `.docx` e `.pdf`. A principal funcionalidade é a **diarização**, que identifica e rotula diferentes locutores na gravação, tornando a transcrição muito mais organizada e útil para reuniões, entrevistas ou podcasts.

O script utiliza as seguintes bibliotecas de código aberto:

- **Whisper da OpenAI:** Para a transcrição de fala para texto.
- **Pyannote.audio:** Para a diarização (identificação dos locutores).
- **PyDub e FFmpeg:** Para manipulação e conversão de arquivos de áudio.
- **python-docx e fpdf:** Para gerar os documentos de saída nos formatos `.docx` e `.pdf`.
- **Tkinter:** Para fornecer uma interface gráfica simples para a seleção do arquivo de áudio.

## Recursos

- **Transcrição de Áudio:** Converte áudio MP3 em texto.
- **Identificação de Locutores:** Rótulos como "NARRADOR 1", "NARRADOR 2" são adicionados à transcrição para cada segmento de fala.
- **Saída em Múltiplos Formatos:** Gera os resultados em arquivos `.docx` e `.pdf` de forma automática.
- **Interface Gráfica Simples:** Uma janela de seleção de arquivo é exibida para facilitar o uso.
- **Aceleração por GPU:** Suporte nativo para usar a GPU (placas NVIDIA com CUDA) para um processamento significativamente mais rápido. O script detecta automaticamente se uma GPU está disponível.

## Requisitos

Para executar este script, você precisará ter o **FFmpeg** instalado e acessível no `PATH` do seu sistema operacional, além de um token de acesso do **Hugging Face**.

1.  **FFmpeg:** Uma ferramenta essencial para a conversão de áudio.
    -   **Windows:** [FFmpeg.org](https://www.ffmpeg.org/download.html)
    -   **Linux (Ubuntu/Debian):** `sudo apt update && sudo apt install ffmpeg`
    -   **macOS:** `brew install ffmpeg` (usando Homebrew)

2.  **Token do Hugging Face:** Necessário para baixar o modelo de diarização da biblioteca `pyannote.audio`. Siga as instruções abaixo para obter o seu.

## Instalação

Siga os passos para configurar o ambiente e instalar todas as dependências.

### 1. Clonar o Repositório (Opcional)

Se você estiver em um repositório Git, pode começar clonando-o:

```bash
git clone [https://github.com/seu-usuario/seu-repositorio.git](https://github.com/seu-usuario/seu-repositorio.git)
cd seu-repositorio




Criar um Ambiente Virtual (Recomendado)
É uma boa prática criar um ambiente virtual para isolar as dependências do projeto.

python -m venv venv
# No Windows
venv\Scripts\activate
# No macOS/Linux
source venv/bin/activate



Instalar as Dependências
Instale todas as bibliotecas necessárias usando pip.

pip install torch torchaudio python-dotenv openai-whisper pyannote.audio pydub python-docx fpdf2

Observação: Se você planeja usar a GPU, a instalação do torch deve ser feita com a versão compatível com sua versão do CUDA. Visite a página de instalação do PyTorch para o comando correto. Exemplo para CUDA 11.8:
pip install torch==2.0.1+cu118 torchaudio==2.0.2+cu118 --index-url https://download.pytorch.org/whl/cu118






Como Obter o Token do Hugging Face
O modelo de diarização pyannote/speaker-diarization-3.1 exige autenticação. Siga estes passos para obter seu token:

Crie uma conta no Hugging Face.

Aceite os termos de uso do modelo pyannote/speaker-diarization-3.1 neste link.

Vá para a sua página de "Settings" e clique em "Access Tokens".

Crie um novo token ou copie um token existente com permissão de "Read" (Leitura).

Abra o arquivo transcrever_audio.py e substitua "COLE_SEU_TOKEN_DO_HUGGING_FACE_AQUI" na variável HF_TOKEN pelo seu token


# No arquivo transcrever_audio.py
HF_TOKEN = "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" # Substitua por seu token real




Uso
Para usar o script, simplesmente execute o arquivo Python. Uma janela de seleção de arquivo será exibida para que você possa escolher o arquivo MP3 a ser processado.

python transcrever_audio.py







O script irá:

Converter o arquivo MP3 para WAV, se necessário.

Executar a diarização para identificar os locutores.

Transcrever o áudio usando o modelo Whisper.

Combinar os resultados, associando cada segmento de fala ao seu respectivo locutor.

Salvar a transcrição completa e formatada em dois arquivos: [nome_do_arquivo].docx e [nome_do_arquivo].pdf.

Possíveis Erros e Soluções
"ffmpeg: not found": Este erro indica que o FFmpeg não está instalado ou não está no seu PATH. Certifique-se de que a instalação foi concluída corretamente.

"ERRO: Por favor, insira seu token de acesso do Hugging Face...": Este é um erro personalizado do script. Ele ocorre se você não substituiu o valor padrão da variável HF_TOKEN no código. Siga as instruções para obter e inserir seu token.

"PyTorch not compiled with CUDA enabled": Este erro significa que a versão do PyTorch instalada não suporta aceleração por GPU. Se você tem uma placa NVIDIA e deseja usar a GPU, reinstale o PyTorch seguindo as instruções da página de instalação do PyTorch com o comando correto para sua versão do CUDA.

Processamento Lento: Se o script estiver rodando na CPU, a transcrição de arquivos grandes pode levar bastante tempo. Verifique se o PyTorch foi instalado com suporte para CUDA e se a sua GPU está sendo detectada. A mensagem Usando dispositivo: cuda no console confirma o uso da GPU.







