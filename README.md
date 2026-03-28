# Site Farinha

Site de apresentação do **Farinha**, software livre para gestão de acervos em arquivos permanentes e memoriais.

🌐 **[farinha.info](https://farinha.info)**

---

## Sobre o Farinha

O Farinha é uma plataforma para entidades de custódia que precisam gerenciar acervos de valor histórico com precisão técnica. Suporta fundos descritos com Nobrade, coleções com metadados personalizados, objetos digitais (textuais, imagéticos, sonoros e audiovisuais) e múltiplas instituições em uma única infraestrutura.

- 📖 **Documentação:** [docs.farinha.info](https://docs.farinha.info)
- 💻 **Código-fonte:** [gitlab.com/yndexa/farinha](https://gitlab.com/yndexa/farinha)
- 📸 **Instagram:** [@farinha.info](https://instagram.com/farinha.info)
- 📧 **Contato:** contato@farinha.info
- 🏢 **Serviços:** [yndexa.com](https://yndexa.com)

---

## Sobre este repositório

Este repositório contém exclusivamente o site de apresentação — uma página HTML estática.

### Estrutura

```
├── index.html          # site completo (arquivo único)
├── img/
│   ├── logo.svg
│   ├── carrossel1.png
│   ├── carrossel2.png
│   ├── caracteristicas.png
│   ├── objetos-digitais.png
│   ├── ricardo.png
│   ├── pablo.png
│   ├── beatriz.png
│   └── cristian.png
└── CLAUDE.md           # instruções para Claude Code
```

### Rodar localmente

```bash
python -m http.server 8080
# acesse http://localhost:8080
```

### Tecnologias

- [Tailwind CSS](https://tailwindcss.com) via CDN
- [Plus Jakarta Sans](https://fonts.google.com/specimen/Plus+Jakarta+Sans) e [Inter](https://fonts.google.com/specimen/Inter) (Google Fonts)
- [Material Symbols](https://fonts.google.com/icons) (ícones)
- Vanilla JS — sem frameworks

### Idiomas

O site está disponível em **Português (PT-BR)**, **Inglês (EN)**, **Espanhol (ES)** e **Romeno (RO)**, com detecção automática do idioma do navegador.

---

## Equipe

| Nome | Papel |
|------|-------|
| Ricardo Sodré Andrade | Coordenador |
| Pablo Soares | Desenvolvedor Sênior |
| Beatriz Azevedo | Desenvolvedora |
| Cristian Privat | Gerente de Projeto |

---

## Licença

Software livre — veja o repositório principal em [gitlab.com/yndexa/farinha](https://gitlab.com/yndexa/farinha).

---

🤖 Criado com auxílio do Claude Code
