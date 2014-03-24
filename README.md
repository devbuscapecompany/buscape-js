Classe BuscapeAPI
========================

Descrição
---------

A classe __BuscapeAPI__ foi criada para ajudar no desenvolvimento de aplicações usando os webservices disponibilizados pela __API do BuscaPé__.

Como funciona ?
---------------

A classe BuscapeAPI __pré-configura__ sua aplicação para uma integração com a API do BuscaPé, ou seja, ela __facilita a integração e agiliza o desenvolvimento__ das aplicações.

Como Usar ?
-----------

> Defina um diretório para ela em sua aplicação.

	mkdir buscape-js

> Faça um clone do repositório

	git clone https://github.com/devbuscapecompany/buscape-js.git

> Instancie a classe.
> Use sua instância criada para chamar os métodos da classe.

	var objBuscaPeApi = new BuscapeAPI( applicationID , sourceID );
			
	objBuscaPeApi.setSandbox();
	objBuscaPeApi.findCategoryList( { categoryId : 0 } );

Para mais informações acesse o [guia do desenvolvedor BuscaPé](http://developer.buscape.com/api/)

Métodos de Criação de código Lomadee
====================================

String BuscapeAPi::createSource( Object args )
-----------------------------------------------------

Serviço utilizado somente na integração do Aplicativo com o Lomadee.

Dentro do fluxo de integração, o aplicativo utiliza esse serviço para criar sourceId (código) para o Publisher que deseja utiliza-lo.
Os parâmetros necessários neste serviço são informados pelo __próprio Lomadee ao aplicativo.__

_No ambiente de homologação sandbox, os valores dos parâmetros podem ser fictícios pois neste ambiente este serviço retornará sempre o mesmo sourceId para os testes do Developer._

Todos os parâmetros necessários para a busca são informados em um objeto que deve ser passado para o método, são eles:

* __sourceName__ Nome do código.
* __publisherId__ ID do publisher.
* __siteId__ ID do site selecionado pelo publisher.
* __campaignList__ Lista de IDs das campanhas __separados por vírgula__.
* __token__ Token utilizado para validação da requisição.

Recuperação dos dados
=====================

void BuscapeAPI::receiveContent( Object result )
------------------------------------------------

O retorno de todas as chamadas serão recebidos pelo método BuscapeAPI.receiveContent que receberá como
parâmetro o objeto JSON retornado pela API.

	var objBuscaPeApi = new BuscapeAPI( applicationID , sourceID );
	
	objBuscaPeApi.findCategoryList( { categoryId : 0 } );
	objBuscaPeApi.receiveContent = function( result ) {
		alert( result.details.message );
	}; 

Métodos de Consulta Disponíveis
===============================

String BuscapeAPi::findCategoryList( Object args )
--------------------------------------------------

Método faz busca de categorias, permite que você exiba informações relativas às categorias.
É possível obter categorias, produtos ou ofertas informando apenas um ID de categoria.

Todos os parâmetros necessários para a busca são informados em um objeto que deve ser passado para o método, são eles:

* __categoryId__ Id da categoria.
* __keyword__ Palavra-chave buscada entre as categorias.
* __callback__ Função de retorno a ser executada caso esteja usando o método __JSON__ como retorno.

Se não for informado nenhum dos parâmetros, a função retornará por padrão uma lista de categorias raiz, de id 0.

void BuscapeAPi::findOfferList( Object args , Boolean lomadee )
---------------------------------------------------------------

Método busca uma lista de ofertas.
É possível obter a lista de ofertas informando o ID do produto.

Todos os parâmetros necessários para a busca são informados em um objeto que deve ser passado para o método, são eles:

* __categoryId__ Id da categoria.
* __keyword__ Palavra-chave buscada entre as categorias.
* __productId__ Id do produto.
* __barcode__ Código de barras do produto.
* __callback__ Função de retorno a ser executada caso esteja usando o método __JSON__ como retorno.

O parâmetro lomadee é um boolean que indicará se será utilizada a API Lomadee, por padrão esse valor é false.

Pelo menos um dos parâmetros de pesquisa devem ser informados para o retorno da função. Os parâmetros __categoryId__ e __keyword__ podem ser usados em conjunto.

void BuscapeAPi::findProductList( Object args , Boolean lomadee )
-----------------------------------------------------------------

Método permite que você busque uma lista de produtos únicos utilizando o id da categoria final ou um conjunto de palavras-chaves ou ambos.
Todos os parâmetros necessários para a busca são informados em um objeto que deve ser passado para o método, são eles:

* __categoryId__ Id da categoria.
* __keyword__ Palavra-chave buscada entre as categorias.
* __callback__ Função de retorno a ser executada caso esteja usando o método __JSON__ como retorno.

Pelo menos um dos parâmetros, __categoryID__ ou __keyword__ são requeridos para funcionamento desta função. Os dois também podem ser usados em conjunto.
Ou seja, podemos buscar uma palavra-chave em apenas uma determinada categoria.

O parâmetro lomadee é um boolean que indicará se será utilizada a API Lomadee, por padrão esse valor é false.

void BuscapeAPi::topProducts( Object args )
-------------------------------------------

Método retorna os produtos mais populares do BuscaPé.
Todos os parâmetros necessários para a busca são informados em um objeto que deve ser passado para o método, são eles:

* __callback__ Função de retorno a ser executada caso esteja usando o método __JSON__ como retorno.

void BuscapeAPi::viewProductDetails( Object args )
--------------------------------------------------

Função retorna os detalhes técnicos de um determinado produto.
Todos os parâmetros necessários para a busca são informados em um objeto que deve ser passado para o método, são eles:

* __productId__ Id do produto _(requerido)_.
* __callback__ Função de retorno a ser executada caso esteja usando o método json como retorno.

void BuscapeAPi::viewSellerDetails( Object args )
-------------------------------------------------

Função retorna os detalhes da loja/empresa como: endereços, telefones de contato etc...
Todos os parâmetros necessários para a busca são informados em um objeto que deve ser passado para o método, são eles:

* __sellerId__ Id da loja/empresa _(requerido)_.
* __callback__ Função de retorno a ser executada caso esteja usando o método __JSON__ como retorno.

void BuscapeAPi::viewUserRatings( Object args )
-----------------------------------------------

Método retorna as avaliações dos usuários sobre um determinado produto.
Todos os parâmetros necessários para a busca são informados em um objeto que deve ser passado para o método, são eles:

* __productId__ Id do produto _(requerido)_.
* __callback__ Função de retorno a ser executada caso esteja usando o método __JSON__ como retorno.

Getters, Setters e Métodos auxiliares
=====================================

String BuscapeAPi::getApplicationId()
-------------------------------------

Retorna o Id da aplicação.

Veja também BuscapeAPI::setApplicationId( String applicationId )

String BuscapeAPi::getCountryCode()
-----------------------------------

Retorna o código do país.

Veja também BuscapeAPI::setCountryCode( String countryCode )

String BuscapeAPi::getEnvironment()
-----------------------------------

Retorna o ambiente de integração (_bws_ para produção e _sandbox_ para testes).

Veja também BuscapeAPI::setSandbox()

String BuscapeAPi::getFormat()
------------------------------

Retorna o formato de retorno (_xml_ ou _json_).

Veja também BuscapeAPI::setFormat( String format )

String BuscapeAPi::getSourceId()
--------------------------------

Retorna o Source ID.

Veja também BuscapeAPI::setSourceId( String sourceId )

void BuscapeAPI::setApplicationId( String applicationId )
---------------------------------------------------------

Define o Id da aplicação.

* _String_ __applicationId__ ID da aplicação registrado no BuscaPé.

Para obter um ID de aplicação você precisará fazer seu [registro](http://developer.buscape.com/admin/registration.html)

Veja também BuscapeAPI::getApplicationId()

void BuscapeAPI::setCountryCode( String countryCode )
-----------------------------------------------------

Define o código do país.

* _String_ __countryCode_ Código do país, pode ser um dos abaixo:
	* __AR__ Para Argentina
	* __BR__ Para Brasil
	* __CL__ Para Chile
	* __CO__ Para Colômbia
	* __MX__ Para México
	* __PE__ Para Peru
	* __VE__ Para Venezuela


Veja também BuscapeAPI::getCountryCode()

void BuscapeAPI::setFormat( String format )
-------------------------------------------

Define o formato de retorno.

* _String_ __format__ Formato do retorno, pode ser __xml__ ou __json__

Veja também BuscapeAPI::getFormat()

void BuscapeAPI::setSandbox( void )
-----------------------------------

Define se a integração vai ser feita no sandbox ou no ambiente de produção.

Veja também BuscapeAPI::getEnvironment()

void BuscapeAPI::setSourceId( String sourceId )
-----------------------------------------------

Define o sourceId

* _String_ __sourceId__ O sourceId

Veja também BuscapeAPI::getSourceId()