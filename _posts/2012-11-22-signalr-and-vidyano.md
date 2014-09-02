---
title: SignalR and Vidyano
author: Steve Hansen
layout: post
permalink: /2012/11/22/signalr-and-vidyano/
tags:
  - Learning Japanese
  - SignalR
  - Vidyano
---
After the announcement of David Fowler about the new release of [SignalR][1], I had to try it out on my Learning Japanese web app ([latest commit][2]). I&#8217;ve started with basic chat app and added some Vidyano related calls to it (it will automatically translate between English <-> Japanese).

So first I had to add the correct NuGet package to the Web site, instead of the App_Start code I&#8217;ve changed the Vidyano code to map the WebAPI routes in the [Global.asax.cs][3] because I already had the file.

{% highlight csharp %}protected void Application_Start(object sender, EventArgs e)
{
    RouteTable.Routes.MapHubs(); 
    Vidyano.Service.WebControllerFactory.RegisterRoutes();
}{% endhighlight %}

With SignalR they have added a MapHubs extension method, in Vidyano we can use the WebControllerFactory&#8217;s RegisterRoutes to do the same. SignalR comes first because it&#8217;ll handle the /signalr paths, and Vidyano handles the rest.

My hub is mostly the basic chat hub which can be found in the [Chat.cs][4] file:

{% highlight csharp %}public class Chat : Hub
{
    public void Send(string userName, string message)
    {
        if (string.IsNullOrEmpty(userName))
            userName = "<anonymous>";

        if (string.IsNullOrEmpty(message))
            message = "<empty>";

        string[] translations;
        if (JapaneseKanaClassifier.ContainsJapaneseScript(message))
            translations = Manager.Current.GetTranslations(new[] { message }, "ja", "en");
        else
            translations = Manager.Current.GetTranslations(new[] { message }, "en", "ja");

        var clientMessage = Manager.Current.GetTranslatedMessage("UserSays", userName, message, translations.Length < 0 ? translations[0] : "<unknown>");
        Clients.All.addMessage(clientMessage);
    }
}{% endhighlight %}

My JapaneseKanaClassifier class is used to see if the message contains any Japanese characters (Kanji, Hiragana or Katakana) and if so it will be translated to English, otherwise it will assume that it is in English and it will be translated to Japanese.

That was all that was needed for the service side part, but I&#8217;ve also used the [Vidyano Web class][5] to add the needed JavaScripts for the Client part by adding the jquery.signalR-1.0.0-alpha1.min.js embedded with my other scripts, and adding the necessary <script src="/signalr/hubs" to my html.

As for the client, I&#8217;ve used a virtual persistent object Chat to view it in my application and the Chat template is using the following:

{% highlight html %}<script type="text/javascript">
  $(function () {
    var chat = $.connection.chat;
    chat.client.addMessage = function (message) {
      $('#messages').append('<li>' + message.replace('\n', '<br>') + '</li>');
    };

    function send(){
      chat.server.send(app.friendlyUserName, $('#msg').val());
      $('#msg').val('');
    };

    $("#broadcast").on("click", send);
    $("#msg").on("keypress", function (e) {
      if ((e.keyCode || e.which) == 13)
        send();
    });

    $.connection.hub.start();

    $("#msg").focus();
  });
</script>

<div>
  <ul id="messages"></ul>
  <input type="text" id="msg" />
  <input type="button" id="broadcast" value="<%= app.getTranslatedMessage('Say') %>" />
</div>{% endhighlight %}

Again nothing special, when clicking on the Say button, or pressing Return it will send the message and the current friendlyUserName to the service.

You can check it all out on <http://vidyano.apphb.com/#!/Chat>

 [1]: http://weblogs.asp.net/davidfowler/archive/2012/11/11/microsoft-asp-net-signalr.aspx
 [2]: https://bitbucket.org/Hansen/learningjapanese/changeset/70fa42ad576b3d94d27b2ae00027495f
 [3]: https://bitbucket.org/Hansen/learningjapanese/src/70fa42ad576b3d94d27b2ae00027495f527f06a3/LearningJapanese.Service.Web/Global.asax.cs
 [4]: https://bitbucket.org/Hansen/learningjapanese/src/70fa42ad576b3d94d27b2ae00027495f527f06a3/LearningJapanese.Service/Chat.cs
 [5]: https://bitbucket.org/Hansen/learningjapanese/src/70fa42ad576b3d94d27b2ae00027495f527f06a3/LearningJapanese.Service/LearningJapaneseWeb.cs