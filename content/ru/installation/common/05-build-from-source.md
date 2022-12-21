## Сборка из исходников

Чтобы собрать Hugo из исходников, вы должны:

1. Установить [Git]
1. Установить [Go] версии 1.18 или выше.
1. Обновить переменную окружения PATH, как описано в [документации Go].

> Директория установки контролируется переменными окружения GOPATH и GOBIN. Если определена переменная GOBIN, двоичные файлы устанавливаются в эту директорию. Если задана GOPATH, двоичные файлы устанавливаются в поддиректорию bin первого каталога в списке GOPATH. В противном случае двоичные файлы устанавливаются в поддиректорию bin GOPATH по умолчанию ($HOME/go или %USERPROFILE%\go).

Затем соберите и протестируйте:

```sh
go install -tags extended github.com/gohugoio/hugo@latest
hugo version
```

[Git]: https://git-scm.com/book/en/v2/Getting-Started-Installing-Git
[Go]: https://go.dev/doc/install
[документации Go]: https://go.dev/doc/code#Command
