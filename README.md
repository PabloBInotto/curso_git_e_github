# curso_git_e_github
Este é um repositório apenas para teste e treinamento relacionado ao curso de Git e GitHub;

# Status

Não monitorado (Untracked).

Monitorado (Tracked):

> git init [inicia repositório git];

> git add fileName.ext [adiciona arquivo para rastreamento];

> git commit -m "Mensagem" [Adiciona o a repositório];

Modificado (Modified):

:: Após cada alteração necessário realizar novamente os passos anteriores.

> git add fileName.ext [adiciona arquivo para rastreamento];

> git commit -m "Mensagem" [Adiciona o a repositório];

Finalizado (Staged):
> git pull

# Adicionar usuários

> git config user.name "nome do usuário"
> git config user.email "email@usuario.com"

# verificar os commits realizados

> git log :: mostra todos os commits
> git log --oneline :: mostra o resumo de cada commit em uma única linha
> git log -n (n = número inteiro) :: mostra os últimos commits com base no número (n) passado
> git log --before "aaaa-mm-dd" :: mostra os commits de um antes da data informada
> git log --after "aaa-mm-dd" :: mostra os commits após a data informada
> git log --since= "2 days ago"
> git log --author "nome" :: realiza a consulta e mostra todos os commits de determinado autor
> git log --email

para ter uma lista completa de todas as flags possíveis usar o comando: git help log

# Voltando no tempo como o git
Toda vez que um commit é realizado, é gerado uma hash e através dela é possível verificar o status do projeto naquele momento.

> git checkout hash (substituir hash com a hash desejada)

Para retornar ao status atual do projeto
> git checkout master>

Para verificar se existem pendências
> git status

Para renomear um projeto (like linux)
git mv nome_atual novo_nome

Para deletar um arquivo
> git rm nome_do_arquivo

*** Importante ***

A cada arquivo modificado é fundamental realizar o "add" e "commit". Isso facilita na resolução de erros e no gerenciamento do projeto como um todo;

*** end ***

Antes do commit é uma boa pratica verificar as modificações que foram realizadas e se essas estão de acordo com os objetivos a serem alcançados:

> git diff --staged

Também é possível realizar por hash

> git diff hash_mais_antiga..hash_mais_nova

*** Nota *** 

Para finalizar as consultas digite a letra "q"!

*** end ***

Se foi detectado algum erro após a realização do commit, isso pode ser corrigido adicionando a flag --amend:

> git commit --amend -m "mensagem"

É possível também retornar o arquivo para o status co commit anterior:
> git checkout nomeDoArquivo.ext

Tirar um arquivo do status Staged para Unstaged:
> git restore --staged nomeDoArquivo.ext

Caso seja cometidos muitos erros e não foi possível identificá-los, é possível retornar todos sos arquivos para o status do ultimo commit:
>  git reset HEAD --hard

Ou pode ser foito somente os que foram commitados (ficou legal essa nova palavra "Commitado" :)
> git reset HEAD^ --hard

# Fim da seção 3 e inicio da Seção 4:
Cada branch é uma ramifica~ção do projeto principal
                                    Nova Branch      base
Ex: Linha da vida do projeto ---------|---------------|----------------------> 
                                    base            Nova Branch     

Para criar uma nova branch (ramificação) de um projeto:
> git checkout -b nome_da_branch

OBS.: Todas as modificações realizadas na nova branch não alteram a branch principal (master).

Para deletar uma branch:
git branch -d nome_da_brach

Para fazer a união de duas branch:
> gir merge nome_da_branch
OBS.: Você deve estar com o terminal dentro da branch onde a outra branch será incluída.
      Após realizar o merge e os testes de funcionalidade, a branch que foi incluída pode ser deletada.

Para fazer a união de uma branch na base onde ela foi iniciada.
> git rebase NomeDaBranch

Para clonar um repositório
git clone url/nomeDoRepositório.git .

OBS.: O "." ao fim do comando é para que a clonagem seja feita na pasta local, sem o ponto será criado uma pasta com o nome idêntico ao do projeto clonado.

Para enviar arquivos ao repositório
> git push origin master
OBS.: Deve ser um repositório BARE

Para baixar as atualização do repositório tem duas opção:
Opção 1:
 > git fetch
 > git rebase

 Opção 2 (essa é melhor pois faz o fatch e o rebase de uma só vez, não é necessário realizar o dois comandos):
> git pull -u origin master

# Implementação de um repositório "BARE"

> git init --bare
^ Esse será o repositório principal, de onde outros usuários vão clonar e atualizar remotamente

Use o comando push para enviar atualizações e pull para baixar as atualização feitas por outros usuários;

# incluir um colaborador no projeto

Menu settings>Manage Access>Invite a collaborator>
 --> Incluir nome no usuário no github ou email e enviar o convite.

# Tags

As tags sevem para guardar o projeto em um determinado status.
Para criar uma tag
> git tag v1.0

para enviar uma tag
> git push origin v1.0

Para verificar os arquivos da versão da tag
> git checkout v1.0

Para retornar a versão de desenvolvimento
> git checkout master

è possível realizar as alterações/correções na versão implementada e atualizar a tag
> git switch -c correções-v1.0
Apos as correções
> git add....
> git commit ...
> git merge ou rebase
Gere a nova tag
> git tag v1.1
E para finalizar as atualizações, envie para o repositório principal
> git push origin v1.1

# desfazer alterações realizadas
Quando é feito modificações e não foi feito o add e commit. É possível retornar todos ao estado original como comando
> git checkout -- .

Caso você saiba exatamente qual é o arquivo, o estado original pode ser re-estabelecida com o comando abaixo:
> git checkout -- nomeDoArquivo.ext

Para desfazer depois de enviar os arquivos para o repositório
> git checkout HEAD --.
Isso faz o repositório retornar ao estado anterior ao commit e exclui as alterações de todos os arquivos modificados.
Para fazer o procedimento e excluir as modificações de um arquivo especifico, é só informar o nome do arquivo.
> git checkout HEAD -- nomeDoArquivo.ext

# Revert
Usar o revert as modificações e inclui um novo commit
> git revert hashID

# git reset
O reset exclui o commit que foi realizado anteriormente
> git reset HEAD~1
O número 1 se refere à quantos commits serão excluídos e por isso deve ser utilizado com muito cuidado.

# resolvendo conflitos
Geralmente um conflito ocorre ao realizar o merge ou o push e quando duas pessoas realizam modificações no mesmo arquivo antes de ter atualizado e tenta submeter para o repositório.
É muito importante prestar a atenção nas mensagens que o git passa a cada ação realizada.
Muitas vezes as mensagens são passadas, mas sem o destaque de uma mensagem de erro.
A resolução de conflitos é feito pelo desenvolvedor, que deve decidir quais ações serão tomadas em relação ao código;
Não há uma receita, pois, cada conflito terá uma resolução diferente e conta com o nível de conhecimento do desenvolvedor em relação ao código e ao projeto como um todo, dessa forma resolver o conflito considerando o comportamento esperado para a aplicação em questão.

# Push rejeitado
Caso o repositório local esteja desatualizado em relação ao repositório remoto, ao realizar o push vai o correr a rejeição;
Para resolver é necessário primeiramente realizar a atualização (pull)
Após a atualização o push será realizado com sucesso.
Para evitar essa situação ao trabalhar com um grupo onde os arquivos são alterados com muita frequência, o ideal é realizar a atualização (pull) antes de enviar (push) os arquivos para o repositório remoto.

# Histórico usando a interface gráfica:

Uso de interface gráfica também é muito importante o desenvolvedor saber utilizar:
Toda visualização gráfica é realizado no próprio site do github.

# Gerenciar repositório pelo VS-code

É possível realizar todos os passos e ações que foram realizado por comandos com os atalhos da IDE VS-Code

# Colaborando com projeto Open Source
1 - Descobrindo e avaliando Projetos
2 - Trabalhando com Issues
3 - Trabalhado com Fork
4 - Realizando Pull Request
5 - Workflow padrão do github
6 - Verificando e aceitando Pull Request

# Fluxo de trabalho do github
https://guides.github.com/introduction/flow/

Understanding the GitHub flow
GitHub flow is a lightweight, branch-based workflow that supports teams and projects where deployments are made regularly. This guide explains how and why GitHub flow works.

1 - Create a branch;
2 - Add commits;
3 - Open a Pull Request;
4 - Discuss and review your code;
5 - Deploy (With GitHub, you can deploy from a branch for final testing in production before merging to main.);
6 - Merge;

# Git no VS-code
Para facilitar o gerenciamento da atividades usando o Git no VS-Code vamos instalar duas extenções:
GitHistory e Gitlens;
Opcionalmente também pode instalar o GitGraph <-- esse é chapado!

# Criação de um currículo online
Clonar o repositório CV-Online e mude o nome da pasta para o seu nome de usuário;

Criar um repositório na sua conta do github com a seguinte nomenclatura (seuUsuárioNoGithub.github.io) <-- não pode errar essa parte!!

> git config user.name "UsuárioGitHub" // registro do usuário
> git config user.email "seuemail@mail.com" // registro do email do usuário
Delete o bloco de dados [remote "origin"] do arquio config da pasta .git (Pasta oculta) para cadastrar a nova origin
> git remote add origin https://github.com/UsuarioGitHub/UsuarioGitHub.github.io.git // Fazer o setup da origem do repositório... é necessário mudar
Caso você tenha o Python (se não tiver é so instalar, não é nao?) rode o seguinte comendo para levantar um servidor e visualizar essa pagina que estamos desenvolvendo em http://localhost:8000
> python -m SimpleHTTPServer 8000
Após isso abra um navegador e acesse a sua página. Isso é legal para visualizar e fazer todos so testes necessários.
Caso não queira abrir dessa forma, é só ir até a pasta do arquivo e abrir o arquivo index.html com um navegador web de sua preferência.

…or create a new repository on the command line
echo "# test" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/PabloBInotto/test.git
git push -u origin main
…or push an existing repository from the command line
git remote add origin https://github.com/PabloBInotto/test.git
git branch -M main
git push -u origin main
