# Etapa 1: build da aplicação
FROM node:18-alpine AS build-stage
WORKDIR /app

# Copia os arquivos de dependência
COPY package*.json ./
COPY . .

# Instala dependências e gera a build
RUN npm install
RUN npm run build

# Etapa 2: imagem de produção com Nginx
FROM nginx:1.19.3-alpine AS production-stage

# Copia os arquivos da build para o diretório servido pelo Nginx
COPY --from=build-stage /app/.next/server/app /usr/share/nginx/html

# Expõe a porta padrão do Nginx
EXPOSE 80

# Inicia o Nginx em primeiro plano
CMD ["nginx", "-g", "daemon off;"]
