##HOMEWORK (Cross-site scripting)
#Installing
Follow this guide => [https://github.com/plataformatec/devise]()

After generate User devise
 
```bash
$ rails g scffold Blogs content:text user:references 
$ rake db:migrate
```
Go to application_controller.rb then add content below to force user to login first

```before_action :authenticate_user!```

Run server and create user account

Change Code to following box below 
 
Type ```<script>window.alert("sometext")</script>``` in comment box


1.Original

```ruby
<p>
  <strong>Content:</strong>
  <%= @blog.content %>
</p>
```
2.Raw

```ruby
<p>
  <strong>Content:</strong>
  <%= raw @blog.content %>
</p>
```
3.Two equal sign

```ruby
<p>
  <strong>Content:</strong>
  <%== @blog.content %>
</p>
```

4..html_safe

```ruby
<p>
  <strong>Content:</strong>
  <%= @blog.content.html_safe %>
</p>
```
5.Sanitize

```ruby
<p>
  <strong>Content:</strong>
  <%= sanitize @blog.content %>
</p>
```

###Conclusion

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;After putting javascript or html code, with code 2,3,4 will tricker alert box which is not good! first box I think it already secure by it self. However, the safest among 2,3,4 and 5 it's turn out that only Sanitize did not tricker alert box.