
from moviepy import *
from PIL import Image, ImageDraw, ImageFont
import numpy as np

# CONFIGURAÇÕES
W, H = 1080, 1920
DURACAO = 60
CENAS = [
    ("O APOCALIPSE COMEÇOU", "O mundo pode mudar em segundos."),
    ("REGRA 1", "Mantenha a calma."),
    ("REGRA 2", "Procure um abrigo seguro."),
    ("REGRA 3", "Garanta água e alimentos."),
    ("REGRA 4", "Mantenha contato com pessoas confiáveis."),
    ("REGRA 5", "Evite confrontos desnecessários."),
    ("SOBREVIVA", "Pense antes de agir.")
]

def criar_cena(titulo, texto, duracao):
    img = Image.new("RGB", (W, H), (12, 15, 20))
    draw = ImageDraw.Draw(img)

    try:
        fonte_titulo = ImageFont.truetype(
            "DejaVuSans-Bold.ttf", 75
        )
        fonte_texto = ImageFont.truetype(
            "DejaVuSans.ttf", 42
        )
    except:
        fonte_titulo = ImageFont.load_default()
        fonte_texto = ImageFont.load_default()

    draw.text((70, 750), titulo, font=fonte_titulo,
              fill=(220, 35, 35))
    draw.text((70, 900), texto, font=fonte_texto,
              fill=(255, 255, 255))

    return ImageClip(np.array(img)).with_duration(duracao)

# CRIAR CENAS
clips = []
tempo = DURACAO / len(CENAS)

for titulo, texto in CENAS:
    cena = criar_cena(titulo, texto, tempo)
    clips.append(cena)

# MONTAR VÍDEO
video = concatenate_videoclips(clips)

# EXPORTAR
video.write_videofile(
    "apocalipse_zumbi.mp4",
    fps=30,
    codec="libx264",
    audio=False
)

print("Vídeo criado com sucesso!")
# reels-studio
Editor de vídeos para reels
