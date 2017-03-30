---
title: has_secure_token para criar chaves únicas - Rails 5
---

Finalmente temos uma solução nativa do Rails para gerar chaves seguras, sem precisar instalar dependências ou criar strings randômicas. A solução está no `has_secure_token`.

<!--more-->

Foi [adicionado o método has_secure_token](https://github.com/rails/rails/pull/18217) no Active Record que permite gerar um token facilmente numa coluna padrão ou específica (quando informada), diretamente no model.

{% highlight ruby %}
class User < ApplicationRecord
  has_secure_token
end
{% endhighlight %}

O código acima  prevê que exista a coluna `token` na tabela do modelo `User`, pois por padrão, quando o registro é salvo, ele cria o token justamente neste campo. Na prática:

```
>> user = User.new
>> user.save
=> true

>> user.token
=> '77TMHrHJFvFDwodq8w7Ev2m7'
```

Você também pode passar um símbolo como parâmetro para o método.

{% highlight ruby %}
class User < ApplicationRecord
  has_secure_token :auth_token
end
{% endhighlight %}

Assim, setará um token para a coluna `auth_token`, e não na coluna `token` como é feito por padrão.

### Método `regenerate_token`

Adicionado o método `has_secure_token` no model, também lhe dá um método `regenerate_token`, inclusive baseado no parâmetro que você atribuir. No caso, se você setou no model `has_secure_token :auth_token`, você terá o método `regenerate_auth_token`.

```
>> user.auth_token
=> "77TMHrHJFvFDwodq8w7Ev2m7"

>> user.regenerate_auth_token
=> true

>> user.auth_token
=> "wodq8w7Ev2m787TMHrHJFvFD"
```

## Fazendo isso no Rails 4.x

Com um pouco mais de verbosidade, você pode ter este mesmo comportamento no Rails 4.x.

{% highlight ruby %}
class User < ActiveRecord::Base
  before_save :set_secure_token

  private
  def set_secure_token
    self.token = generate_token
  end

  def generate_token
    loop do
      token = SecureRandom.hex(10)
      break token unless User.where(access_token: token).exists?
    end
  end
end
{% endhighlight %}

Pra quê isso tudo? rs

Referência de [has_secure_token](http://api.rubyonrails.org/classes/ActiveRecord/SecureToken/ClassMethods.html#method-i-has_secure_token) na API do Rails 5.
