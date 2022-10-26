# Dagger
Roteiro Laboratório de Engenharia de Software - “Usando o Framework Dagger para Injeção de Dependência”
Integrantes: Henrique Pereira Cristófaro, Matheus Freire Henrique Fonseca e Vitor Theodoro Rocha Domingues

Esse roteiro tem como objetivo introduzir a utilização do Dagger para a injeção de dependência, nele iremos explicar rapidamente conceitos básicos antes de partirmos para a utilização do framework em si.

## O que é dependência?

Em programação, dependência é a utilização de uma classe pela outra.

Ex.: 

Existem duas classes: Carro e Veículo. Supondo que um veículo possa instanciar um objeto do tipo carro, a classe veículo depende de Carro e a classe Carro vira uma dependência de veículo.


class Veiculo{
    Carro carro;
    Veiculo(){
    carro = new Carro(); #é como se sempre que criássemos um veículo nós construíssemos um   carro
   }
}

A injeção de dependência com o mesmo exemplo seria algo do tipo:

class Veiculo{
    Carro carro;
    Veiculo(Carro carro){
        this.carro = carro; #A injeção de dependência é uma modificação positiva, pois faz com que o objeto de dependência, nesse caso o carro, possa ser facilmente           alterado. Além disso, diminui a responsabilidade da classe Veiculo sendo assim, criando classes mais enxutas.
    }
}

## Por que usar o Dagger?

No exemplo acima, vimos como funcionaria a injeção de dependência para um exemplo simples, quando possuímos apenas Carro e Veículo, mas o que ocorreria, se por exemplo, possuíssemos Motocicleta, Ônibus, Avião, Trem, Barco, Bicicleta…, ou seja, um número muito grande de dependências? Bom, sem a utilização de um framework como o Dagger, nós iríamos possuir um código extenso e complicado que se fosse utilizado em mais de um lugar no projeto ficaria repetido, ou seja, se precisássemos fazer uma alteração precisaríamos de alterar mannualmente em cada parte do programa em que o trecho aparece.  Para evitar o trabalho repetitivo, utilizamos esse framework que simplifica de forma expressiva a tarefa. 

## Como utilizar o Dagger

Você pode acessar o link  https://github.com/google/dagger se quiser seguir o tutorial feito pela Google, mas iremos demonstrar o passo a passo abaixo:

Observação: Para esse tutorial iremos utilizar o Android Studio, logo assumiremos que o usuário tem ele instalado. Se não possuir, baixe nesse link: [https://developer.android.com/studio](https://developer.android.com/studio)

### Adicionando o Dagger em um projeto

Para se utilizar o Dagger, devemos instalá-lo no nosso projeto. Para isso, vamos importar o framework utilizando o gradle ([What is Gradle?](https://docs.gradle.org/current/userguide/what_is_gradle.html)).

1. Crie um projeto no Android Studio (Empty Activity > Language: Java)
2. Acesse o build.graddle(Project:)

![image](https://user-images.githubusercontent.com/91568652/197934643-81652290-3268-4a77-a370-90e1cf6b8052.png)


3. Utilize o seguinte código para puxar o dagger: 

buildscript{
    ext{
        compose_version = '1.1.0'
    }
    dependencies{
        classpath "com.google.dagger:hilt-android-gradle-plugin:2.40.5"
    }
}

- Exemplo de como ficou a classe:

![image](https://user-images.githubusercontent.com/91568652/197934804-b5a9746e-848e-4d02-a844-8ec13ec55307.png)

4. Acesse o build.gradle (Module: App)
    
![image](https://user-images.githubusercontent.com/91568652/197934831-4dacde9d-65ac-491b-b846-0046444a00a0.png)

    
5. Insira os seguintes plugins no campo plugins{}

id ‘kotlin-kapt’

id ‘dagger.hilt.android.plugin’

6. Cole o código a seguir no campo dependencies {}.

//Dagger - Hilt

implementation "com.google.dagger:hilt-android:2.40.5”

kapt "com.google.dagger:hilt-android-compiler:2.40.5”

implementation "androidx.hilt:hilt-lifecycle-viewmodel:1.0.0-alpha03”

kapt "androidx.hilt:hilt-compiler:1.0.0”

implementation 'androidx.hilt:hilt-navigation-compose:1.0.0’

Pronto, agora o seu projeto já possui o Dagger.

### Utilizando na prática

Para utilizar o Dagger, além de instalá-lo precisamos também de organizar o projeto para isso. Sendo assim alguns passos devem ser seguidos para que se possa utilizar o Dagger em um projeto:

- iremos utilizar o exemplo já descrito no inicio do roteiro:

Veículos: Carro, Moto, Avião…

- Construindo a classe Veículos:

Instanciamos todos os elementos “veículos” e geramos suas dependências criando um construtor, para que assim, a classe veículo não seja responsável por essa tarefa. Além disso, usamos o método função para validar que a Classe foi instanciada.

![image](https://user-images.githubusercontent.com/91568652/197943595-eaabbb34-5928-4472-968a-0ff4b36b2984.png)


- MainActivity:

é na Classe MainActivity que iremos utilizar a classe Veiculo, chamamos a classe veiculo e sua função posteriormente.

![image](https://user-images.githubusercontent.com/91568652/197943799-3df74b5e-5c4b-4d09-836b-ba1d0b440167.png)


- VeiculoEspecifico

Como desejamos que o dagger crie nossas dependências para nós, criamos uma Interface chamada VeiculoEspecifico para que essa mande nossos objetos instanciados. Essa é a parte mais importante do projeto que irá criar, armazenar e enviar os dados necessários.

![image](https://user-images.githubusercontent.com/91568652/197943866-18ef4325-4513-4f25-99c9-724f6c2c0d57.png)
O dagger irá configurar a função. Devemos utilizar o @ Component para que seja gerado.

Após essa configuração inicial do Dagger, devemos voltar na Classe Veículo e definir onde será o inject. Da seguinte forma: 

![image](https://user-images.githubusercontent.com/91568652/197943928-538274f0-2d8a-48cf-98dd-a75de2cb9564.png)

isso, para que o Dagger saiba onde ele deve fazer a injeção.

Da mesma forma, devemos configurar o Dagger para Carro, Moto e avião:
![image](https://user-images.githubusercontent.com/91568652/197943990-2f00e2bf-3e0a-48cc-a8f0-eb9458737965.png)

Finalmente, como última alteração, vamos na MainActivity e criamos uma instância de um Veículo Especifico: 

![image](https://user-images.githubusercontent.com/91568652/197944030-2a3a6455-b472-4246-bddc-0cfdfb33ee91.png)


Executando o programa obtemos como saída do log: 

![image](https://user-images.githubusercontent.com/91568652/197944071-06af87a8-7c9f-46df-a943-dd109cfaf9c5.png)

o que prova que a classe foi devidamente instanciada.

###Adendo

Podemos observar também, algumas estruturas do Dagger como a DaggerVeiculoEspecifico, que é uma classe gerada pelo Daggere mostra a construção dos componentes. Demonstrando assim um dos maiores benefícios do Dagger, a criação desse extenso código que seria feito pelo programador, mas que é gerado assim que se compila o código.

![image](https://user-images.githubusercontent.com/91568652/197944146-a28d79ee-15ee-48eb-a69e-524741177ef3.png)

