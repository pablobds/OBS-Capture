# OBS-Capture


# 🚀 OBS-CAPTURE (60 FPS Low Overhead ARM)

Script em Shell otimizado para **captura e transmissão de tela em tempo real** no ambiente **Linux & Termux** via servidor gráfico X11 (VNC/XFCE/Proot). 

Ele transmite o vídeo com latência ultra baixa via UDP, utilizando flags cirúrgicas do FFmpeg para não sobrecarregar o processador (CPU ARM) do celular.

---

## ⚡ Principais Recursos

- **60 FPS com Latência Quase Nula (Zero Latency):** Configurações refinadas do `x264` desativam filtros pesados de pós-processamento (como *deblock* e *b-frames*), reduzindo o uso de CPU e eliminando o atraso no vídeo.
- **2 Modos de Captura:**
  - **Modo 1 (Tela Cheia):** Captura toda a área do display `:1`.
  - **Modo 2 (Janela com Auto-Reload):** Permite clicar na janela desejada dentro do VNC/XFCE para capturar apenas ela.
- **Auto-Recuperação de Resolução:** Se a janela capturada for redimensionada, o script recalcula a resolução e reinicia a captura automaticamente sem travar.
- **Cálculo de Proporção Par:** Corrige larguras e alturas ímpares em tempo real via matemática de shell, evitando erros do codec `YUV420p` sem gastar CPU com filtros de escala (`scale filter`).
- **Gerenciamento Inteligente de Processos:** Limpa processos zumbis do FFmpeg e evita conflitos de porta ocupada (`Address already in use`).


---

## 📋 Pré-requisitos

Certifique-se de ter os pacotes necessários instalados no seu Termux:

```bash
pkg update && pkg install ffmpeg x11-utils -y
```

```bash
chmod +x obs
```

```bash
./obs
```




## Como Assistir / Conectar no OBS
Assim que a transmissão iniciar, abra o seu player de preferência:

Via MPV (Terminal / PC):
```Bash
mpv udp://@127.0.0.1:9999 --no-cache --untimed
```

Via VLC:
- Vá em Mídia > Abrir Fluxo de Rede...
- Insira o endereço: udp://@127.0.0.1:9999
- Clique em Reproduzir.
  
No OBS Studio (PC/Servidor):
- Adicione uma fonte do tipo Fonte de Mídia (Media Source).
- Desmarque a opção Arquivo Local.
- No campo Entrada, coloque: udp://127.0.0.1:9999 (ou o IP do celular na sua rede local).

