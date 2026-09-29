# Caixa Lucrativo — Landing Page (HTML estático)

Projeto pronto para subir no GitHub e publicar no Dokploy.

## Estrutura
- `index.html` — página única
- `assets/` — imagens/ícones extraídos do PDF

## Rodar local (sem instalar nada)
Abra o `index.html` no navegador **ou** use um servidor simples:

### Node
```bash
npx serve .
```

### Python
```bash
python -m http.server 8080
```

Acesse: http://localhost:8080

## Deploy no Dokploy (recomendado)
Use o `Dockerfile` (Nginx) para servir o site.
- Porta padrão do container: **80**
