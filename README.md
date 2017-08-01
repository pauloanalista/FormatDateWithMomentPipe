# FormatDateWithMomentPipe
Pipe criado para formatar datas usando moment no Angular.

## Problema
O pipe foi criado para sanar um problema que tive na hora de formatar datas em meu app feito em Ionic.
Meu JSON retornava uma data no formato 2017-08-01 00:00:00 e ao usar a formatação do angular 

{{escala.data | date : 'dd/MM/yyyy' }} no android retornava 01/08/2017 e no iOS 31/07/2017, isso devido a hora estar zerada, ou seja, no iOS esta pegando 3 horas atrás.

Para resolver o problema criei um pipe que usa a formatação da biblioteca [momentjs](https://momentjs.com/)


## Instalação
Execute no prompt de comando a instalação do moment.

```sh
npm install moment --save

```

Logo em seguida use o ionic CLI para criar um pipe com o seguinte comando

```sh
ionic generate pipe formatDateWithMoment

```

Abra o arquivo gerado que fica dentro da pasta pipes e substitua pelo código abaixo:

```sh
import { Pipe, PipeTransform } from '@angular/core';
import * as moment from 'moment';
@Pipe({
  name: 'formatDateWithMoment',
})
export class FormatDateWithMomentPipe implements PipeTransform {
  transform(value: Date, ...args) {
    return this.formataDataParaExibicao(value, args[0]);
  }

  formataDataParaExibicao(data, format) : string {
    return moment(data).format(format);
  }
}

```

Agora só falta aplicar na sua view o pipe criado na data desejada.

```sh
<p class="itemValue">{{escala.data | formatDateWithMoment : 'DD/MM/YYYY' }}</p>

```

Agora basta passar um formato de data que o moment aceita para trabalhar da forma correta.

