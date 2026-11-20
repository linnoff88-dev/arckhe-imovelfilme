# ðŸ  imovelfilme

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="48" />
  <p><strong>Arckhé AI</strong></p>
</div>


[![Seu anÃºncio vira filme](guia/assets/banner.jpg)](https://inematds.github.io/imovelfilme/guia/)

**ðŸ‡§ðŸ‡· [PortuguÃªs](README.md) Â· ðŸ‡ºðŸ‡¸ [English](README.en.md) Â· ðŸ‡ªðŸ‡¸ [EspaÃ±ol](README.es.md)**

## O que Ã©

O imovelfilme Ã© uma ferramenta gratuita que transforma o anÃºncio de um imÃ³vel num vÃ­deo curto de divulgaÃ§Ã£o. Serve para corretor, imobiliÃ¡ria ou dono que quer postar o imÃ³vel nas redes sem contratar fotÃ³grafo nem editor. VocÃª informa o link; ele lÃª os dados que estÃ£o no anÃºncio, melhora as fotos, cria versÃµes decoradas dos cÃ´modos e monta um filme de 30 segundos com trilha. Precisa de um computador com Python, Node.js, FFmpeg e o Codex logado na sua assinatura.

## ðŸ“– Guia de uso

Guia completo (landing + passo a passo + vÃ­deo): **https://inematds.github.io/imovelfilme/guia/**

## Como funciona

```
link do anÃºncio â†’ dados verificados â†’ atÃ© 10 fotos â†’ foto profissional â†’ decoraÃ§Ã£o virtual â†’ brief â†’ filme MP4
```

1. **Ler o anÃºncio** (`engine/extrair.py`): JSON-LD, `og:`, marcaÃ§Ãµes `data-imovel` e texto da pÃ¡gina. Cada campo guarda a fonte; o que nÃ£o estÃ¡ no anÃºncio fica de fora.
2. **Fotos** (`engine/fotos.py`): atÃ© 10, uma por cÃ´modo antes de repetir. O Codex (`image_gen`, pela assinatura) faz a versÃ£o profissional de cada foto e a decoraÃ§Ã£o virtual de sala, cozinha e quartos. A cor Ã© neutralizada (o gerador puxa para o amarelo).
3. **Brief** (`engine/brief.py`): 4 a 8 fatos fortes (quartos, Ã¡rea, banheiros, vagas, destaques).
4. **Filme** (`engine/video.py`): composiÃ§Ã£o HyperFrames (HTML + GSAP) â†’ MP4 16:9 ou 9:16; trilha mixada a âˆ’14 LUFS.

## Uso

```bash
git clone https://github.com/inematds/imovelfilme && cd imovelfilme
npm i
python3 imovelfilme.py estilos
python3 imovelfilme.py tudo "https://seusite.com.br/imoveis/apto-1202" --projeto ~/imoveis/apto1202 \
  --estilo praia-contemporaneo --trilha assets/trilhas/elegante.mp3
```

Etapas soltas: `extrair`, `fotos`, `brief`, `video` (mesmos parÃ¢metros). A pasta do imÃ³vel fica assim:

```
apto1202/
  imovel/anuncio.json  brief.json  brief.md
  fotos/original/  profissional/  decorada/
  video/16x9/        (composiÃ§Ã£o HyperFrames)
  output/filme-16x9.mp4
```

## Demo

`samples/anuncio-demo/` Ã© um anÃºncio **fictÃ­cio** (fotos geradas por IA) para testar sem depender de site de terceiros:

```bash
python3 -m http.server 8941 --directory samples/anuncio-demo &
python3 imovelfilme.py tudo http://127.0.0.1:8941/ --projeto projetos/demo --trilha assets/trilhas/elegante.mp3
```

O vÃ­deo de apresentaÃ§Ã£o (`promo/promo.py`) Ã© feito com o prÃ³prio motor a partir do resultado do demo.

## Regras

- Nada inventado: campo ausente no anÃºncio nÃ£o aparece no vÃ­deo.
- Foto profissional e decoraÃ§Ã£o virtual nÃ£o mudam parede, janela, porta, piso, bancada, sacada nem vista.
- Quando hÃ¡ cÃ´modo decorado, o fecho do vÃ­deo avisa: "Imagens tratadas por IA Â· cÃ´modos com decoraÃ§Ã£o virtual".
- Use fotos que vocÃª pode publicar. Marca d'Ã¡gua sÃ³ sai de foto sua ou autorizada.
- Portais que carregam as fotos por script: salve a pÃ¡gina e passe o `.html`.

## Testes

```bash
python3 -m unittest discover -s tests
```

## LicenÃ§a

MIT. Fontes Sora e Inter: SIL OFL 1.1. Trilhas em `assets/trilhas/`: geradas localmente com o MusicGen-small (modelo CC-BY-NC; uso nÃ£o comercial).

---

[INEMA.CLUB](https://inema.club)

---

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="32" />
  <p><strong>Arckhé AI</strong></p>
</div>