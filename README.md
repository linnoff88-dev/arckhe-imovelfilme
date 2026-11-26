ï»¿# ê°Å¸ÂÂ  imovelfilme

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="48" />
  <p><strong>Arckhé AI</strong></p>
</div>


[![Seu anêÂºncio vira filme](guia/assets/banner.jpg)](https://linnoff88-dev.github.io/arckhe-/guia/)

**ê°Å¸â¡Â§ê°Å¸â¡Â· [PortuguêÂªs](README.md) êÂ· ê°Å¸â¡Âºê°Å¸â¡Â¸ [English](README.en.md) êÂ· ê°Å¸â¡Âªê°Å¸â¡Â¸ [EspaêÂ±ol](README.es.md)**

## O que êÂ©

O imovelfilme êÂ© uma ferramenta gratuita que transforma o anêÂºncio de um imêÂ³vel num vêÂ­deo curto de divulgaêÂ§êÂ£o. Serve para corretor, imobiliêÂ¡ria ou dono que quer postar o imêÂ³vel nas redes sem contratar fotêÂ³grafo nem editor. VocêÂª informa o link; ele lêÂª os dados que estêÂ£o no anêÂºncio, melhora as fotos, cria versêÂµes decoradas dos cêÂ´modos e monta um filme de 30 segundos com trilha. Precisa de um computador com Python, Node.js, FFmpeg e o Codex logado na sua assinatura.

## ê°Å¸ââ Guia de uso

Guia completo (landing + passo a passo + vêÂ­deo): **https://linnoff88-dev.github.io/arckhe-/guia/**

## Como funciona

```
link do anêÂºncio ê¢â â dados verificados ê¢â â atêÂ© 10 fotos ê¢â â foto profissional ê¢â â decoraêÂ§êÂ£o virtual ê¢â â brief ê¢â â filme MP4
```

1. **Ler o anêÂºncio** (`engine/extrair.py`): JSON-LD, `og:`, marcaêÂ§êÂµes `data-imovel` e texto da pêÂ¡gina. Cada campo guarda a fonte; o que nêÂ£o estêÂ¡ no anêÂºncio fica de fora.
2. **Fotos** (`engine/fotos.py`): atêÂ© 10, uma por cêÂ´modo antes de repetir. O Codex (`image_gen`, pela assinatura) faz a versêÂ£o profissional de cada foto e a decoraêÂ§êÂ£o virtual de sala, cozinha e quartos. A cor êÂ© neutralizada (o gerador puxa para o amarelo).
3. **Brief** (`engine/brief.py`): 4 a 8 fatos fortes (quartos, êÂ¡rea, banheiros, vagas, destaques).
4. **Filme** (`engine/video.py`): composiêÂ§êÂ£o HyperFrames (HTML + GSAP) ê¢â â MP4 16:9 ou 9:16; trilha mixada a ê¢Ëâ14 LUFS.

## Uso

```bash
git clone https://github.com/linnoff88-dev/imovelfilme && cd imovelfilme
npm i
python3 imovelfilme.py estilos
python3 imovelfilme.py tudo "https://seusite.com.br/imoveis/apto-1202" --projeto ~/imoveis/apto1202 \
  --estilo praia-contemporaneo --trilha assets/trilhas/elegante.mp3
```

Etapas soltas: `extrair`, `fotos`, `brief`, `video` (mesmos parêÂ¢metros). A pasta do imêÂ³vel fica assim:

```
apto1202/
  imovel/anuncio.json  brief.json  brief.md
  fotos/original/  profissional/  decorada/
  video/16x9/        (composiêÂ§êÂ£o HyperFrames)
  output/filme-16x9.mp4
```

## Demo

`samples/anuncio-demo/` êÂ© um anêÂºncio **fictêÂ­cio** (fotos geradas por IA) para testar sem depender de site de terceiros:

```bash
python3 -m http.server 8941 --directory samples/anuncio-demo &
python3 imovelfilme.py tudo http://127.0.0.1:8941/ --projeto projetos/demo --trilha assets/trilhas/elegante.mp3
```

O vêÂ­deo de apresentaêÂ§êÂ£o (`promo/promo.py`) êÂ© feito com o prêÂ³prio motor a partir do resultado do demo.

## Regras

- Nada inventado: campo ausente no anêÂºncio nêÂ£o aparece no vêÂ­deo.
- Foto profissional e decoraêÂ§êÂ£o virtual nêÂ£o mudam parede, janela, porta, piso, bancada, sacada nem vista.
- Quando hêÂ¡ cêÂ´modo decorado, o fecho do vêÂ­deo avisa: "Imagens tratadas por IA êÂ· cêÂ´modos com decoraêÂ§êÂ£o virtual".
- Use fotos que vocêÂª pode publicar. Marca d'êÂ¡gua sêÂ³ sai de foto sua ou autorizada.
- Portais que carregam as fotos por script: salve a pêÂ¡gina e passe o `.html`.

## Testes

```bash
python3 -m unittest discover -s tests
```

## LicenêÂ§a

MIT. Fontes Sora e Inter: SIL OFL 1.1. Trilhas em `assets/trilhas/`: geradas localmente com o MusicGen-small (modelo CC-BY-NC; uso nêÂ£o comercial).

---

[ARCKHÉ AI](https://ARCKHÉ AI)

---

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="32" />
  <p><strong>Arckhé AI</strong></p>
</div>