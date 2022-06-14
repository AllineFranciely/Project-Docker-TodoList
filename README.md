Primeiro projeto do módulo de backend do curso da Trybe.
Nesse projeto necessitei Conteinerizar aplicações; Criar uma conexão entre elas; Orquestrar seu funcionamento.

Foi dada uma aplicação full-stack neste repositório: um **aplicativo de tarefas**! Esta aplicação necessitou ser conteinerizada para funcionar. Tive que desenvolver os arquivos de configuração para cada frente específica: `Front-end`, `Back-end` e,  para um aplicativo de `teste` que valida se as aplicações estão se comunicando.

Foi necessário criar as imagens para as aplicações e configurar essas imagens com o `docker-compose`.

Para isto, foram utilizados uma série de comandos do `docker` com diferentes níveis de complexidade,  cada um escrito em seu próprio arquivo.

Buscou-se atender os seguintes requisitos:

1. Crie um container em modo interativo, sem rodá-lo, nomeando-o como `01container` e utilizando a imagem `alpine` na versão `3.12`
- O `nome` do container deve ser `01container`;
- O container deve usar a imagem `alpine` na versão `3.12`;
- O `status` do container deve ser `created`;
- O container **não deve** estar em execução após ter sido criado.

2. Inicie o container `01container`
- O avaliador verificará se o container está parado;
- O avaliador executará o comando criado neste requisito;
- O container **deve** estar em execução.

3. Liste os containers filtrando pelo nome `01container`
- O comando deve retornar uma lista contendo informações **apenas** do `01container`.

4. Execute o comando `cat /etc/os-release` no container `01container` sem se acoplar a ele
- Que o comando retornará os dados corretos da `distro` no container:
- `NAME="Alpine Linux"`
- `ID=alpine`
- `VERSION_ID=3.12`

5. Remova o container `01container`
- O avaliador rodará o comando 5;
- O avaliador validará o processo com o comando 3.

6. Faça o download da imagem `nginx` com a versão `1.21.3-alpine` sem criar ou rodar um container
- Que a imagem correta foi baixada;
- Que nenhum container foi iniciado para isso.

7. Rode um novo container com a imagem  `nginx` com a versão `1.21.3-alpine` em segundo plano nomeando-o como `02images` e mapeando sua porta padrão de acesso para porta `3000` do sistema hospedeiro
- Que o container foi iniciado corretamente;
- Que é possível ter acesso ao container pelo endereço `localhost:3000`;
- Que a página retorna o valor esperado.

8. Pare o container `02images` que está em andamento
- Que não há nenhum container ativo após seu comando.

9. Gere uma build a partir do Dockerfile do `back-end` do `todo-app` nomeando a imagem para `todobackend`
- Se existe um arquivo `Dockerfile` em `./docker/todo-app/back-end/`:
  - O Dockerfile deve rodar uma imagem `node` utilizando a versão `14`;
    - Recomenda-se o uso da variante `-alpine`, pois ela é otimizada para desempenho;
    - Lembre-se de consultar o README do `todo-app` para validar os requisitos da aplicação.
  - Deve estar com a porta `3001` exposta;
  - Deve adicionar o arquivo `node_modules.tar.gz` a imagem;
  - Deve copiar todos os arquivos da pasta `back-end` para a imagem;
  - Ao iniciar a imagem deve rodar o comando `npm start`.
- Se ao *buildar* o Dockerfile o nome da imagem gerada é igual a `todobackend`.

10. Gere uma build a partir do Dockerfile do `front-end` do `todo-app` nomeando a imagem para `todofrontend`
- Se existe um arquivo `Dockerfile` em `./docker/todo-app/front-end/`:
    - O `Dockerfile` pode rodar uma imagem `node` utilizando a versão `14`;
      - Recomenda-se o uso da variante `-alpine`, pois ela é otimizada para desempenho;
      - Lembre-se de consultar o README do `todo-app` para validar os requisitos da aplicação.
    - Deve estar com a porta `3000` exposta;
    - Deve adicionar o arquivo `node_modules.tar.gz` a imagem, de maneira que ele seja extraído dentro do `container`;
    - Deve copiar todos os arquivos da pasta `front-end` para a imagem;
    - Ao iniciar a imagem deve rodar o comando `npm start`;
  - Se ao *buildar* o `Dockerfile` o nome da imagem gerada é igual a `todofrontend`.

11. Gere uma build a partir do Dockerfile dos `testes` do `todo-app` nomeando a imagem para `todotests`
- Se existe um arquivo `Dockerfile` em `./docker/todo-app/tests/`:
  - O Dockerfile deve rodar a imagem `mjgargani/puppeteer:trybe1.0` para que os testes funcionem;
  - Deve adicionar o arquivo `node_modules.tar.gz` a imagem;
  - Deve copiar todos os arquivos da pasta `tests` para a imagem;
  - Ao iniciar a imagem deve rodar o comando `npm test`;
- Se ao *buildar* o Dockerfile o nome da imagem gerada é igual a `todotests`.

# Requisito bônus do projeto

12. Suba uma orquestração em segundo plano com o docker-compose de forma que `backend`, `frontend` e `tests` consigam se comunicar
- O container de `todotests` deve ter como dependencia os containers `frontend` e `backend`;
- O nome do _service_ deverá ser `todotests`;
- Deve ter uma variável de ambiente `FRONT_HOST` que recebe como valor o nome do container do `frontend`
  - Lembrando que, dentro de uma rede docker, o host de um container é indentificado pelo seu nome.

##### front-end

- O container de `todofrontend` deve rodar na porta `3000`;
- O nome do _service_ deverá ser `todofront`;
- Deve ter como dependencia o container `backend`;
- Deve ter uma variável de ambiente `REACT_APP_API_HOST` que recebe como valor o nome do container do `backend`.
  - Lembrando que, dentro de uma rede docker, o host de um container é indentificado pelo seu nome.

##### back-end

- O container de `todobackend` deve rodar na porta `3001`;
- O nome do _service_ deverá ser `todoback`;

