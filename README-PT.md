# Teste para engenheiro de dados

## Introdução
A Chama é uma empresa moderna que tem como base do seu negócio apps no [IOS](https://itunes.apple.com/BR/app/id1228143385?mt=8), [Android](https://play.google.com/store/apps/details?id=br.project.pine) e recentemente e fase de experimentação, a versão [web](https://app.chama.com.br/offer?lat=-23.5854852&lon=-46.6790965&houseNumber=940&streetName=Rua%2520Joaquim%2520Floriano&subLocality=Itaim%2520Bibi&postalCode=04534-004&adminArea=S%25C3%25A3o%2520Paulo&subAdminArea=S%25C3%25A3o%2520Paulo).
Esta realidade obriga-nos a fazer um esforço especial para colectar toda a informação possível e fazer com que esteja disponível para toda a empresa.
Parte da informação é gerada pelas nossas apps e o nosso backend. Outro tipo de informação vem de fontes como a Google Play Store que nos traz informação bastante útil relativamente à app performance e classificação por parte dos usuários.
Esta empresa é muito _data-driven_ e, como tal, as decisões são tomadas com base nas métricas apropriadas. A qualidade dos dados é uma responsabilidade de todas as pessoas envolvidas.

-----

### Exercício 1: Desinstalação da app
A app usa o _SDK_ do Firebase para reportar os eventos. Nos eventos do Firebase é possível encontrar _DeviceId_ e _InstanceId_.
 - **DeviceId** é um _Id_ único que identifica o aparelho físico, o telefone ou _tablet_ onde a applicação é instalada.
 - **InstanceId** é um _Id_ novo para cada vez que o mesmo _device_ instala a aplicação. Ou seja, se a aplicação for instalada no mesmo aparelho várias vezes, vamos ver um novo _InstanceId_ e o mesmo _DeviceId_.

A maior parte dos eventos contem informação do _DeviceId_ e do _InstanceId_, mas por motivos técnicos, o evento de desinstalação apenas tem o _DeviceId_.

*t1: Eventos de desinstalação*

|DeviceId|EventName|EventDateTime       |
|--------|---------|--------------------|
|DeviceA |uninstall|Dec 4, 2018 10:45:00|
|DeviceB |uninstall|Dec 5, 2018 11:45:00|
|DeviceC |uninstall|Dec 6, 2017 12:45:00|

*t2: Informação de _Device_*

|Instance  |DeviceId|InstanceFirstSeenDateTime|
|----------|--------|-------------------------|
|InstanceA1|DeviceA |Nov 1, 2018 13:45:00     |
|InstanceA2|DeviceA |Dec 2, 2018 14:45:00     |
|InstanceA3|DeviceA |Dec 9, 2018 14:45:00     |
|InstanceB1|DeviceB |Nov 1, 2018 15:45:00     |
|InstanceB2|DeviceB |Dec 4, 2018 16:45:00     |
|InstanceCX|DeviceC |Dec 4, 2018 00:00:00     |

Por motivos mencionados anteriormente, é importante determinar por quanto tempo a aplicações esteve instalada.

***tf**: tabela final de desinstalações:*

|Instance  |DeviceId|EventName|InstanceFirstSeenDateTime|EventDateTime       |
|----------|--------|---------|-------------------------|--------------------|
|InstanceA2|DeviceA |uninstall|2018-12-02 14:45:00      |2018-12-04 10:45:00 |
|InstanceB2|DeviceB |uninstall|2018-12-04 16:45:00      |2018-12-05 11:45:00 |

(Deve incluir o DeviceC ou não consoante a sua opinião)

#### Exercício 1.1: Teoria
O objectivo é criar uma tabela de desinstalações enriquecida, limpa e integra tal como está acima, numa base de dados qualquer para que outros possam aceder a esta informação. **Por favor responda às questões num pequeno parágrafo**
 - Assumindo que a informação está disponível em ficheiros CSV, o tamanho desses ficheiros pode definir a como o trabalho vai ser executado. Por favor explique as diferentes opções que contemplaria.
 - Como reparou, a data não tem o melhor formato para ser _parsed_ como tipo _datetime_, como pode ultrapassar este problema?
 - O DeviceC tem data de desinstalação anterior à data que vemos no [InstanceFirstSeenDateTime].
   - Qual pode ser a causa desta situação?
   - Você incluiria o DeviceC na tabela final de desinstalações? Porquê?

#### Exercício 1.2: Prática
Usando uma base de dados da sua escolha, crie a tabela **tf** onde o seu ponto de partida são os ficheiros [Instances.csv](Instances.csv) e [UninstallEvents.csv](UninstallEvents.csv).
Por favor, na sua solução, **assuma que os ficheiros têm mais do que 1GB**

-----

### Exercício 2: Integração externa
Um fornecedor externo quer enviar informação sobre a opinião das pessoas sobre a empresa Chama e a sua app. Eles oferecem duas opções para enviar a informação.
Uma opção é através de um _POST_ num _URL_ que a Chama disponibilizaria, todas as vezes que algo acontece, em tempo real.
A segunda opção é a Chama fazer _download_ da informação em _bulk_, em formato CSV, uma vez por dia.
**Por favor responda às seguintes questões num pequeno parágrafo**:
 - Qual a opção que escolheria?
 - Quais são as vantagens de cada uma das opções?

Usando o [draw.io](https://www.draw.io/) ou semelhante, por favor desenhe um _flow_ detalhado descrevendo a solução que prefere na importação para a base de dados. Por favor mencione as tecnologias que usaria nos diferentes passos.
