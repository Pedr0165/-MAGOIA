<div align="center">

```
███╗   ███╗ █████╗  ██████╗  ██████╗ 
████╗ ████║██╔══██╗██╔════╝ ██╔═══██╗
██╔████╔██║███████║██║  ███╗██║   ██║
██║╚██╔╝██║██╔══██║██║   ██║██║   ██║
██║ ╚═╝ ██║██║  ██║╚██████╔╝╚██████╔╝
╚═╝     ╚═╝╚═╝  ╚═╝ ╚═════╝  ╚═════╝ 
```

### *Assistente de voz local com IA, personalidade e voz neural em português.*

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Ollama](https://img.shields.io/badge/Ollama-Local_AI-000000?style=for-the-badge&logo=ollama&logoColor=white)
![Edge TTS](https://img.shields.io/badge/Edge_TTS-pt--BR-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![Google STT](https://img.shields.io/badge/Google_STT-Speech-4285F4?style=for-the-badge&logo=google&logoColor=white)
![Status](https://img.shields.io/badge/Status-Online-00ff88?style=for-the-badge)

</div>

---

## ✨ O que é o Mago?

**Mago** é um assistente de voz pessoal que roda o cérebro **100% local na sua máquina** — sem nuvem, sem assinatura, sem custo por uso.

Você fala. Ele ouve. Ele pensa. Ele responde — com **voz neural em português brasileiro**, em tempo real.

A IA por trás do Mago é a **Sexta-Feira**: uma assistente com personalidade rica, capaz de ser parceira, mentora, sarcástica ou executiva — dependendo do que você precisar.

---

## 🔄 Pipeline de funcionamento

```
         Você fala
             │
             ▼
   ┌─────────────────────┐
   │       voz.py        │  🎙️  Grava 5s via microfone (sounddevice)
   │                     │      Transcreve com Google Speech (pt-BR)
   └─────────┬───────────┘
             │  texto transcrito
             ▼
   ┌─────────────────────┐
   │     cerebro.py      │  🧠  Envia ao Qwen 2.5:7b via Ollama
   │                     │      Mantém histórico de até 10 turnos
   └─────────┬───────────┘
             │  resposta em texto
             ▼
   ┌─────────────────────┐
   │    voz_saida.py     │  🔊  Sintetiza voz com pt-BR-AntonioNeural
   │                     │      Reproduz via ffplay (sem interface)
   └─────────────────────┘
             │
             ▼
        Você ouve
```

---

## 🗂️ Estrutura do Projeto

```
📁 Projetos Py/
├── 🚀 main.py          — Loop principal: inicializa e orquestra tudo
├── 🧠 cerebro.py       — Motor de raciocínio (Ollama + Qwen 2.5:7b)
├── 🎙️  voz.py           — Captura de áudio e transcrição (STT)
├── 🔊 voz_saida.py     — Síntese de voz neural em pt-BR (TTS)
└── 📋 OBS.txt          — Instruções de ativação do ambiente
```

---

## 🧠 A IA: Sexta-Feira

O motor do Mago roda o modelo **Qwen 2.5 (7B parâmetros)** localmente via Ollama, com uma personalidade multifacetada chamada **Sexta-Feira**:

| Modo | Descrição |
|------|-----------|
| 🤝 **Parceira** | Leal, acolhedora, cria um ambiente de confiança |
| 💼 **Executiva** | Sofisticada, profissional e refinada |
| 🎯 **Militar** | Tática, precisa e direta ao ponto |
| 😏 **Sarcástica** | Gênio caótico com humor afiado |
| 🌱 **Mentora** | Sábia, guia para evolução pessoal |
| 🔀 **Híbrida** | Adapta-se ao contexto e ao usuário |

---

## 🔧 Stack Técnica

| Módulo | Tecnologia | Detalhe |
|--------|-----------|---------|
| **STT** | `speech_recognition` + Google | Gravação com `sounddevice`, 16kHz mono, 5s por turno |
| **LLM** | `ollama` + `qwen2.5:7b` | 100% local, janela deslizante de 10 turnos |
| **TTS** | `edge-tts` Microsoft Neural | Voz `pt-BR-AntonioNeural`, tom `-15Hz`, ritmo `-10%` |
| **Áudio** | `ffplay` (FFmpeg) | Reprodução por pipe stdin, sem interface gráfica |

> 🔒 **Privacidade:** apenas a transcrição de voz usa o serviço do Google. Todo o raciocínio e a memória da conversa ficam 100% na sua máquina.

---

## 🚀 Como rodar

### Pré-requisitos

```bash
# FFmpeg (para o ffplay)
sudo apt install ffmpeg

# Dependências Python
pip install edge-tts ollama speechrecognition sounddevice numpy
```

### Subir o modelo de IA

```bash
ollama run qwen2.5:7b
```

### Ativar o ambiente e iniciar

```bash
cd "/home/pedro/Área de trabalho/Projetinhos /Projetos Py"
source venv/bin/activate
python3 main.py
```

---

## 💬 Exemplo de uso

```
════════════════════════════════════════
  Mago — Online
════════════════════════════════════════

[Ouvindo...]

[Você]: O que é computação quântica?

[Mago está pensando...]

[Mago]: Computação quântica é o uso de fenômenos da mecânica
quântica — como superposição e entrelaçamento — para processar
informações de formas que computadores clássicos não conseguem.
Em vez de bits (0 ou 1), trabalha com qubits, que podem ser
os dois ao mesmo tempo. Ainda está longe do uso cotidiano,
mas para problemas específicos, é absurdamente mais rápida.
```

---

## ⚙️ Ajustes e Configurações

### Voz (`voz_saida.py`)

```python
VOZ        = "pt-BR-AntonioNeural"  # Única voz masculina neural pt-BR no Edge TTS
VELOCIDADE = "-10%"                  # Mais pausado e deliberado
TOM        = "-15Hz"                 # Tom mais grave (intensifica o efeito)
```

### Reconhecimento de voz (`voz.py`)

```python
DURACAO = 5      # Segundos de gravação por turno — aumente se falar devagar
TAXA    = 16000  # 16kHz — padrão para reconhecimento de fala
```

### Comportamento da IA (`cerebro.py`)

```python
MAX_TURNOS     = 10    # Janela deslizante de memória de conversa
temperature    = 0.9   # Respostas mais criativas e variadas
top_p          = 0.92  # Balanceia coerência e diversidade
repeat_penalty = 1.2   # Evita repetições na resposta
```

---

## 🐛 Problemas comuns

| Problema | Causa provável | Solução |
|----------|---------------|---------|
| `[Erro] Sem conexão com Google Speech` | Sem internet | Verifique sua conexão |
| Sem áudio na resposta | `ffplay` não instalado | `sudo apt install ffmpeg` |
| `ollama.ResponseError` | Modelo não baixado | `ollama run qwen2.5:7b` |
| Microfone não detectado | Dispositivo errado | Ajuste o parâmetro `device` no `sd.rec()` |

---

<div align="center">

*"Pronto para receber ordens."*

**— Sexta-Feira, via Mago**

</div>
