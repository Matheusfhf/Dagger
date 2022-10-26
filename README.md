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

        this.carro = carro; #A injeção de dependência é uma modificação positiva, pois faz com que o objeto de dependência, nesse caso o carro, possa ser facilmente alterado. Além disso, diminui a responsabilidade da classe Veiculo sendo assim, criando classes mais enxutas.

    }
}

## Por que usar o Dagger?

No exemplo acima, vimos como funcionaria a injeção de dependência para um exemplo simples, quando possuímos apenas Carro e Veículo, mas o que ocorreria, se por exemplo, possuíssemos Motocicleta, Ônibus, Avião, Trem, Barco, Bicicleta…, ou seja, um número muito grande de dependências? Bom, sem a utilização de um framework como o Dagger, nós iríamos possuir um código extenso e complicado que se fosse utilizado em mais de um lugar no projeto ficaria repetido, ou seja, se precisássemos fazer uma alteração precisaríamos de alterar mannualmente em cada parte do programa em que o trecho aparece.  Para evitar o trabalho repetitivo, utilizamos esse framework que simplifica de forma expressiva a tarefa. 

## Como utilizar o Dagger

Você pode acessar o link  https://github.com/google/dagger se quiser seguir o tutorial feito pela Google, mas iremos demonstrar o passo a passo abaixo:

Observação: Para esse tutorial iremos utilizar o Android Studio, logo assumiremos que o usuário tem ele instalado. Se não possuir, baixe nesse link: [https://developer.android.com/studio](https://developer.android.com/studio)

### Adicionando o Dagger em um projeto

Para se utilizar o Dagger, devemos instalá-lo no nosso projeto. Para isso, vamos importar o framework utilizando o gradle ([What is Gradle?](https://docs.gradle.org/current/userguide/what_is_gradle.html)).

1. Crie um projeto no Android Studio
2.  Acesse o build.gradle (App)
    
    ![image](https://user-images.githubusercontent.com/91568652/197932277-f7d461a7-3e83-43b4-8b60-0095782ea09b.png)

    
3. Cole o código a seguir no campo dependencies {}.

//Dagger - Hilt

implementation "com.google.dagger:hilt-android:2.40.5”

kapt "com.google.dagger:hilt-android-compiler:2.40.5”

implementation "androidx.hilt:hilt-lifecycle-viewmodel:1.0.0-alpha03”

kapt "androidx.hilt:hilt-compiler:1.0.0”

implementation 'androidx.hilt:hilt-navigation-compose:1.0.0’



Pronto, agora o seu projeto já possui o Dagger.

### Utilizando na prática

Para utilizar o Dagger, além de instalá-lo precisamos também de organizar o projeto para isso. Sendo assim alguns passos devem ser seguidos para que se possa utilizar o Dagger em um projeto:


