---
title: Crie um Experimento com o Azure Machine Learning
description: A Microsoft tem disponível aos assinantes do Azure uma máquina de aprendizado, chamada de Azure Machine Learning, o qual permite simular uma infinidade de cenários estatísticos a partir de uma base de dados. O objetivo deste artigo é guia-los passo a passo na montagem de um experimento através da aplicação de um modelo de regressão linear.
author: Renato Haddad
ms.date: 09/02/2016
ms.topic: how-to-article
ms.service: Azure ML
ms.custom: CommunityDocs
---






#Crie um Experimento com o Azure Machine Learning


##**Renato Haddad**
**MVP ASP.NET /MCP/MCTS/MCPD/RD**
Novembro, 2015

[Blog](http://weblogs.asp.net/renatohaddad/)


A Microsoft tem disponível aos assinantes do Azure uma máquina de aprendizado, chamada de Azure Machine Learning, o qual permite simular uma infinidade de cenários estatísticos a partir de uma base de dados. O objetivo deste artigo é guia-los passo a passo na montagem de um experimento através da aplicação de um modelo de regressão linear.

Tudo começa em https://studio.azureml.net, conforme a figura 1, o qual você deverá se logar com sua conta da Microsoft.

![](./img/pic001.png)

Figura 1 – Tela inicial do Azure Machine Learning

Toda a interface é online, não há nada offline ou local, então na lista de menu na barra superior, você tem a opção chamada Studio (estúdio). Clique nela para acessar a ferramenta, sendo que quando o acesso é feito pela primeira vez ou navega na página principal, é exibida uma janela convidando para um vídeo passo a passo com 5 fases, assim terá uma visão geral. Cabe a você aceitar ou não, eu acho válido para um primeiro contato com o Studio.

A figura 2 mostra a ferramenta Studio com os módulos existentes, os quais descreverei a seguir a funcionalidade de cada um. Esta ferramenta é colaborativa com recursos de arrastar e soltar, configurar propriedades onde você cria, testa e implanta soluções de análise preditiva de dados.

![](./img/pic002.png)

Figura 2 – Módulos existentes

O que contém cada módulo? Vou listar e comentar os 6 módulos disponíveis atualmente.

EXPERIMENTS – é o local onde você cria os experimentos / testes, arrasta componentes para conectá-los a outros, preparar os dados, caso necessário, aplicar modelos para treinar, pontuar, testar e avaliar o experimento, conforme a figura 3.

![](./img/pic003.png)

Figura 3 – Tela de Experimentos

WEB SERVICES – lista de testes publicados que podem ser acessados via Web API ou ferramentas de BI como Excel, através de um token gerado de acordo com a sua conta.

NOTEBOOKS – lista de códigos criados em phyton para auxiliar customizações dos dados nos componentes, conforme a figura 4.

![](./img/pic004.png)

Figura 4 – Código do notebook

DATASETS – lista das fontes de dados que você importou ou fez uso das diversas fontes online disponíveis no próprio Studio. Neste artigo usaremos uma fonte online.

TRAINED MODELS – lista de testes treinados por você a serem aplicados nos componentes.

SETTINGS – dados da sua conta, percentual usado, tokens a serem distribuídos e lista de usuários com acesso aos testes e resultados.



``` C#

public class AdministradorDeArreglos
{
    public bool ExisteEnArreglo(string[] pArreglo, string pPalabra)
    {
        return pArreglo.Any(p => p.ToUpper() == pPalabra.ToUpper());
    }
}
```

Para probar el Código escribimos lo siguiente

``` C#
static void Main(string[] args)
{
    var _administradorDeArreglos = new AdministradorDeArreglos();
    string[] _arreglo = {"Manaza", "Papaya", "Melón", "Sandía", "Piña", "Banano"};
    Console.WriteLine(_administradorDeArreglos.ExisteEnArreglo(_arreglo, "Banano") );
}
```

Y el resultado final será:

![](./img/UnitTest/image1.png)
    

Ahora vamos a proceder a probar el código creando una prueba unitaria.
El primer paso es agregar un proyecto a la solución del tipo Test –&gt;
vamos a utilizar MSTest para hacer las pruebas unitarias en este ejemplo
\[Observación: Yo utilizo Visual Studio Ultimate por lo tanto algunas
opciones de testing pueden no aparecer en otras versiones menores o
pueden estar en otro orden\].

![](./img/UnitTest/image2.png)
    

Como vemos en la siguiente figura, se va a crear un proyecto de testing
que tiene una referencia directa al componente – dll – en donde están
todas las librerías para hacer pruebas unitarias con el MSTest. Además,
se crea un archivo inicial de testing y un grupo de tres “Solution
Items” desde donde vamos a poder configurar y administrar las
funcionalidades de nuestros tests.

![](./img/UnitTest/image3.png)
    

Ahora procedemos a borrar el archivo UnitTest1.cs y vamos a crear uno
desde cero. Luego de borrar el archivo, procedemos a agregar una
referencia al proyecto que queremos probar. Luego damos botón derecho
sobre el proyecto de testing y seleccionamos agregar nuevo test.

![](./img/UnitTest/image4.png)
    

Ahora procedemos a seleccionar el tipo de prueba de unidad que vamos a
crear, en nuestro caso una prueba de unidad básica.

![](./img/UnitTest/image5.png)
    

Este paso nos va a generar un archivo de pruebas básico con un método de
pruebas de ejemplo que cual vamos a proceder a eliminar.

``` C#
using Microsoft.VisualStudio.TestTools.UnitTesting;
namespace Pruebas
{
    [TestClass]
    public class Pruebas_SeriePruebasUnitarias
    {
        [TestMethod]
        public void TestMethod1()
        {

        }
    }
}
```

En el código anterior vemos que la clase generada esta marcada con el
atributo TestClass, esto le indica al motor de pruebas de visual studio
que dentro de esta clase existen pruebas de unidad que debe ejecutar.
Los métodos de prueba son métodos públicos de tipo void que están
marcados por el atributo \[TestMethod\] como se ve en la figura
anterior.

Ahora procedemos a crear nuestra primera prueba unitaria. El código de
la prueba unitaria es el siguiente:

``` C#

[TestClass]
public class Pruebas_SeriePruebasUnitarias
{
    [TestMethod]
    public void ExisteArreglo_RetornaTrue()
    {
        var _administradorDeArreglos = new AdministradorDeArreglos();
        var _resultado = _administradorDeArreglos.ExisteEnArreglo(new[] { "Argentina", "Brasil", "Perú" }, "Brasil");
        Assert.IsTrue(_resultado);
    }
}
```

La prueba unitaria anterior prueba específicamente la unidad de código
“ExisteEnArreglo” de la clase AdministradorDeArreglos.

Al Ejecutar el unit test el resultado será el siguiente:

![](./img/UnitTest/image6.png)
    

Como podemos ver, el test pasó y el panel de resultados de VS así me lo
hace saber.

**Estructura del Unit Test**

Para terminar, es importante notar que los unit test tienen por lo
general una estructura compuesta de tres partes:

Arrange: Es la parte del unit test en donde se configura todo el código
para ejecutar la prueba unitaria. En nuestro caso, el “arrange” es la
creación de la instancia de la clase AdministradorDeArreglos.

Act: Esta es la fase del unit test en donde se ejecuta el código a
probar. En nuestro caso es la invocación del método de instancia
ExisteEnArreglo.

Assert: Es la sección de la prueba unitaria en donde se prueba el
resultado del mismo. En este caso y por lo general, lo hacemos con la
clase Assert –&gt; en MSTest –&gt; y es donde verificamos que la
variable \_resultado == true;


