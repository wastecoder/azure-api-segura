# Protegendo uma API com Azure API Management
Este repositório documenta o processo de aprendizado e aplicação de mecanismos de segurança em uma API simulada utilizando o Azure API Management (APIM),
como parte do desafio de projeto do bootcamp **Azure Cloud Native** da DIO.
Para fins de demonstração, a API expõe informações sobre personagens de Hunter x Hunter.


## :cloud: Recursos Criados no Azure Portal
Durante este projeto, os seguintes recursos foram criados e configurados no Microsoft Azure:

* **Grupo de Recursos:** Contêiner lógico para todos os recursos relacionados a este projeto.
* **Serviço de Gerenciamento de API:** O serviço central para gerenciar, proteger, publicar e analisar a API de personagens.
    * **API Criada:** Dentro do APIM, criei uma API para exibir informações sobre personagens de Hunter x Hunter.
    * **Assinaturas:** Mecanismo utilizado para controlar o acesso à API. Criei novas assinaturas com diferentes escopos, fazendo assim a associação com a API criada e a todas APIs.
    * **Subscriptions da API:** Configurei, no nível da API, o requerimento de uma chave de assinatura para acessar os endpoints.
* **Serviço de Aplicativo:** Plataforma para hospedar aplicações web e APIs.
    * **CORS:** Configurado para permitir acesso à API de diferentes domínios. 
* **Mecanismos de Segurança Implementados (Parcialmente):**
    * **Subscriptions + Assinatura:** O primeiro nível de segurança implementado com sucesso, exigindo uma chave de assinatura para acessar a API através de ferramentas como o Postman.
    * **Validate JWT (Não Concluído):** A intenção era implementar a validação de tokens JWT como uma camada adicional de segurança. Mas, como eu não tenho acesso ao **Microsoft Entra ID**, não consegui criar o ```App Registration``` necessário para configurar essa política no APIM.


## :gear: Processo de Criação da API de Personagens
1.  **Acesso ao Serviço de Gerenciamento de API:** Navegação até o `Serviço de Gerenciamento de API` no Azure Portal.
2.  **Criação da API:** Utilização da opção `HTTP API em Branco` para definir uma nova API para os personagens.
3.  **Definição de Operações (Endpoints):** Criação de duas operações principais.
    * `/personagem/{id}`: Para obter detalhes de um personagem específico.
    * `/personagens`: Para listar todos os personagens (Killua, Gon e Isaac Netero).
4.  **Implementação da Resposta de Mock:** Utilização da política `return-response` na seção `<backend>` de cada operação para retornar um JSON estático representando os dados dos personagens.
5.  **Teste no Portal Azure:** Verificação do funcionamento das APIs diretamente dentro da aba "Teste" do APIM.
6.  **Proteção com Assinatura:** Exploração das configurações de "Subscriptions" no nível da API e a necessidade de incluir a chave de assinatura em requisições externas (como no Postman).


## :bulb: Insights e Possibilidades de Aprendizado
* **Importância do Azure API Management:** O APIM se mostrou uma ferramenta poderosa para gerenciar e proteger APIs, atuando como um ponto de entrada único e permitindo a aplicação de diversas políticas de segurança e transformação.
* **Mecanismos de Segurança em Camadas:** A utilização de Subscriptions e Assinaturas representa uma primeira camada de defesa importante para a API. A intenção de implementar a validação de JWT demonstra a possibilidade de adicionar mais camadas de segurança para uma proteção ainda mais robusta.
* **Simulação de APIs com Políticas:** A capacidade de criar APIs de mock utilizando políticas como `return-response` é extremamente útil para testes e aprendizado, especialmente quando o backend real ainda não está disponível ou o acesso a outros serviços (como o Entra ID) é limitado.
* **Controle de Acesso com Assinaturas:** As assinaturas fornecem um mecanismo robusto para controlar quem pode acessar as APIs e como elas são utilizadas.
* **Chaves de Assinatura por Cliente:** A criação de chaves de assinatura únicas por cliente permite controle de acesso granular, monitoramento detalhado do uso, definição de quotas específicas e maior segurança, facilitando o gerenciamento.
