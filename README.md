Teste Técnico Desenvolvedor(a) Python Júnior [REMOTO]
Neste repositório você encontra o enunciado do teste técnico para a vaga de Desenvolvedor(a) Python Júnior [REMOTO] da Instruct! Você provavelmente chegou aqui através da indicação de alguma pessoa da empresa após passar pelas outras etapas do processo seletivo. Se este não for o seu caso e mesmo assim você implementar alguma solução para este exercício ele não será avaliado.

Você pode usar o problema descrito aqui para exercitar suas habilidades de desenvolvimento, mas a sua solução será avaliada por alguém da Instruct apenas se você estiver no processo seletivo da vaga de Desenvolvedor(a) Python Júnior [REMOTO].

Para saber mais sobre a empresa, leia o FAQ

O problema
A equipe de desenvolvimento Bleeding Edge Enthusiasts (BEE) se orgulha de usar as tecnologias mais recentes e modernas. Essa regra também se aplica aos projetos desenvolvidos em Python pela equipe BEE.

Para garantir que todos seus projetos em Python estão usando as últimas versões disponíves dos pacotes, a equipe pensou em criar uma ferramenta batizada de MagPy. A ferramenta recebe um nome de projeto, uma lista de pacotes e devolve a última versão de cada pacote.

Um dos integrantes da BEE apontou que a API pública do PyPI poderia ser usada para esse fim.

Solução
Você deve desenvolver a MagPy, uma API REST que gerencia uma coleção de projetos. Cada projeto tem um nome e uma lista de pacotes. Cada pacote tem um nome e uma versão.

O cadastro de um projeto recebe o nome e a lista de pacotes. Cada pacote da lista precisa obrigatoriamente especificar um nome, mas a versão é opcional.

Sua API deve validar o projeto cadastrado: todos os pacotes informados devem estar cadastrados no PyPI. Portanto você deve verificar o nome e a versão do pacote.

Quando o pacote vem apenas com o nome, sua API deve assumir que é preciso usar a última versão publicada no PyPI.

Abaixo, alguns exemplos de chamadas que serão feitas nessa API:

POST /api/projects
{
    "name": "titan",
    "packages": [
        {"name": "Django"},
        {"name": "graphene", "version": "2.0"}
    ]
}
O código HTTP de retorno deve ser 201 e o corpo esperado na resposta é:

{
    "name": "titan",
    "packages": [
        {"name": "Django", "version": "3.2.5"},  // Usou a versão mais recente
        {"name": "graphene", "version": "2.0"}   // Manteve a versão especificada
    ]
}
Se um dos pacotes informados não existir, ou uma das versões especificadas for inválida, um erro deve ser retornado.

Para uma chamada semelhante ao exemplo abaixo:

POST /api/projects
{
    "name": "titan",
    "packages": [
        {"name": "pypypypypypypypypypypy"},
        {"name": "graphene", "version": "1900"}
    ]
}
O código HTTP de retorno deve ser 400 e o corpo esperado na resposta é:

{
    "error": "One or more packages doesn't exist"
}
Também deve ser possível visitar projetos previamente cadastrados, usando o nome na URL:

GET /api/projects/titan
{
    "name": "titan",
    "packages": [
        {"name": "Django", "version": "3.2.5"},
        {"name": "graphene", "version": "2.0"}
    ]
}
E deletar projetos pelo nome:

DELETE /api/projects/titan
⚠️	Sua solução deve usar a API pública do PyPI. Não use outro caminho pra buscar as informações necessárias
Esqueleto
Este repositório vem com três esqueletos para iniciar o projeto. Eles já tem algumas partes implementadas e estão prontos para o deploy na Heroku.

Conforme detalhado na próxima seção deste README, nós iremos avaliar a sua API publicada nessa plataforma, então é recomendado que você use uma dessas opções como base para a sua solução.

As opções disponíves estão nas respectivas pastas:

template-django: esqueleto com Django e Django Rest Framework
template-fastapi: esqueleto com FastAPI e SQLAlchemy
template-flask: esqueleto com Flask e SQLAlchemy
Você pode usar outro framework web desde que sua solução use Python. No entanto a configuração do projeto para o deploy será responsabilidade sua. Se você nunca mexeu com nenhuma dessas opções, a recomendação é usar o template-django. Fique à vontade para fazer as alterações que julgar necessárias no código disponibilizado.

Para usar uma dessas bases, você precisará:

Fazer uma cópia da pasta
Iniciar um repositório git nessa pasta
Implementar sua solução
Criar uma conta gratuita no Heroku
Criar um novo app
Seguir as instruções da seção Deploy using Heroku Git
Adicionar o usuário jobs@instruct.com.br como colaborador do app
Avaliação
Num primeiro momento não olharemos o seu código. O projeto será testado de forma automatizada pra checar se implementa a API especificada acima.

Você deve codificar seu projeto em Python e fazer deploy usando os recursos disponibilizados nos Frees Tiers da Heroku.

Quando finalizar a implementação, adicione o usuário com e-mail jobs@instruct.com.br como colaborador do app publicado até o fim do prazo estipulado. Isso nos garante acesso ao endereço em que sua API está publicada, para seguir com os testes automatizados.

⚠️	Você deve adicionar o usuário com e-mail jobs@instruct.com.br no app publicado no Heroku! Não é necessário adicionar acesso ao código fonte num repositório do GitHub.
Nós executaremos dois conjuntos de testes na sua API:

Testes básicos (abertos)
Testes avançados (fechados)
Se a API não passar nos testes básicos, faremos mais duas tentativas. Se mesmo assim ela não passar nos testes básicos nós encerramos os testes.

Se a API passar nos testes básicos e não passar nos testes avançados, faremos mais duas tentativas. Se mesmo assim ela não passar nos testes avançados nós encerramos os testes.

Se a API passar pelos testes avançados nós conferimos superficialmente o seu código para identificar problemas; no entanto você provavelmente já garantiu a sua participação na próxima etapa.

Os testes básicos estão disponíveis neste repositório no arquivo tests-open.js. Use-os durante o desenvolvimento para avaliar se a sua API está correta. Como explicado acima, você não passará para a próxima etapa se a sua solução não atender todos os testes desse arquivo. Use os testes para guiar o desenvolvimento da solução.

Você pode executar esses testes com o k6. Para instalar o k6 basta baixar o binário para o seu sistema operacional (Windows, Linux ou Mac).

Para rodar os testes abertos, especifique a variável de ambiente "API_BASE" com o endereço base da API testada.

Exemplo de aplicação rodando no localhost na porta 8080:

k6 run -e API_BASE='http://localhost:8080/' tests-open.js
Recomendações finais
Não deixe para fazer na última hora
Não teste apenas o Happy Path
Boa sorte!

FAQ
Como me candidatar para trabalhar na Instruct?
As inscrições são feitas através das vagas publicadas no site: https://instruct.com.br/trabalhe-com-a-gente/

Nessa página estão listadas as vagas abertas e todos os detalhes de nosso processo seletivo.

Como ser avisado de novas vagas?
Siga a Instruct no Linkedin.

Sempre publicamos quando novas vagas são abertas.

Como é trabalhar na Instruct?
Você pode ler nosso Handbook. Ele é a referência completa sobre como a Instruct funciona.

Destaque especial para as atribuições do papel de Analista de Desenvolvimento Júnior
