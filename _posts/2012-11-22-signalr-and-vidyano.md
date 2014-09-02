---
title: SignalR and Vidyano
author: Steve Hansen
layout: post
permalink: /2012/11/22/signalr-and-vidyano/
categories:
  - Uncategorized
tags:
  - Learning Japanese
  - SignalR
  - Vidyano
---
After the announcement of David Fowler about the new release of [SignalR][1], I had to try it out on my Learning Japanese web app ([latest commit][2]). I&#8217;ve started with basic chat app and added some Vidyano related calls to it (it will automatically translate between English <-> Japanese).

So first I had to add the correct NuGet package to the Web site, instead of the App_Start code I&#8217;ve changed the Vidyano code to map the WebAPI routes in the [Global.asax.cs][3] because I already had the file.

<pre>protected void Application_Start(object sender, EventArgs e)
<a name="cl-11"></a>{
<a name="cl-12"></a>    RouteTable.Routes.MapHubs(); 
<a name="cl-13"></a>    Vidyano.Service.WebControllerFactory.RegisterRoutes();
<a name="cl-14"></a>}</pre>

With SignalR they have added a MapHubs extension method, in Vidyano we can use the WebControllerFactory&#8217;s RegisterRoutes to do the same. SignalR comes first because it&#8217;ll handle the /signalr paths, and Vidyano handles the rest.

My hub is mostly the basic chat hub which can be found in the [Chat.cs][4] file:

<pre>public class Chat : Hub
<a name="cl-7"></a>    {
<a name="cl-8"></a>        public void Send(string userName, string message)
<a name="cl-9"></a>        {
<a name="cl-10"></a>            if (string.IsNullOrEmpty(userName))
<a name="cl-11"></a>                userName = "&lt;anonymous&gt;";
<a name="cl-12"></a>
<a name="cl-13"></a>            if (string.IsNullOrEmpty(message))
<a name="cl-14"></a>                message = "&lt;empty&gt;";
<a name="cl-15"></a>
<a name="cl-16"></a>            string[] translations;
<a name="cl-17"></a>            if (JapaneseKanaClassifier.ContainsJapaneseScript(message))
<a name="cl-18"></a>                translations = Manager.Current.GetTranslations(new[] { message }, "ja", "en");
<a name="cl-19"></a>            else
<a name="cl-20"></a>                translations = Manager.Current.GetTranslations(new[] { message }, "en", "ja");
<a name="cl-21"></a>
<a name="cl-22"></a>            var clientMessage = Manager.Current.GetTranslatedMessage("UserSays", userName, message, translations.Length &gt; 0 ? translations[0] : "&lt;unknown&gt;");
<a name="cl-23"></a>            Clients.All.addMessage(clientMessage);
<a name="cl-24"></a>        }
<a name="cl-25"></a>    }</pre>

My JapaneseKanaClassifier class is used to see if the message contains any Japanese characters (Kanji, Hiragana or Katakana) and if so it will be translated to English, otherwise it will assume that it is in English and it will be translated to Japanese.

That was all that was needed for the service side part, but I&#8217;ve also used the [Vidyano Web class][5] to add the needed JavaScripts for the Client part by adding the jquery.signalR-1.0.0-alpha1.min.js embedded with my other scripts, and adding the necessary <script src=&#8221;/signalr/hubs&#8221; to my html.

As for the client, I&#8217;ve used a virtual persistent object Chat to view it in my application and the Chat template is using the following:

<pre>&lt;script type="text/javascript"&gt;
$(function () {
var chat = $.connection.chat;
chat.client.addMessage = function (message) {
$('#messages').append('&lt;li&gt;' + message.replace('\n', '&lt;br&gt;') + '&lt;/li&gt;');
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
&lt;/script&gt;

&lt;div&gt;
&lt;ul id="messages"&gt;&lt;/ul&gt;
&lt;input type="text" id="msg" /&gt;
&lt;input type="button" id="broadcast" value="&lt;%= app.getTranslatedMessage('Say') %&gt;" /&gt;
&lt;/div&gt;</pre>

Again nothing special, when clicking on the Say button, or pressing Return it will send the message and the current friendlyUserName to the service.

You can check it all out on <http://vidyano.apphb.com/#!/Chat>

<div class="sharedaddy sd-sharing-enabled">
  <div class="robots-nocontent sd-block sd-social sd-social-official sd-sharing">
    <h3 class="sd-title">
      Share this:
    </h3>
    
    <div class="sd-content">
      <ul>
        <li class="share-email">
          <a rel="nofollow" class="share-email sd-button" href="http://xiu.shoeke.com/2012/11/22/signalr-and-vidyano/?share=email" target="_blank" title="Click to email this to a friend"><span>Email</span></a>
        </li>
        <li class="share-twitter">
          <div class="twitter_button">
          </div>
        </li>
        
        <li class="share-google-plus-1">
          <div class="googleplus1_button">
            <div class="g-plus" data-action="share" data-annotation="bubble" data-href="http://xiu.shoeke.com/2012/11/22/signalr-and-vidyano/">
            </div>
          </div>
        </li>
        
        <li class="share-facebook">
          <div class="like_button">
          </div>
        </li>
        
        <li class="share-linkedin">
          <div class="linkedin_button">
          </div>
        </li>
        
        <li class="share-reddit">
          <div class="reddit_button">
          </div>
        </li>
        
        <li class="share-end">
        </li>
      </ul>
    </div>
  </div>
</div>

 [1]: http://weblogs.asp.net/davidfowler/archive/2012/11/11/microsoft-asp-net-signalr.aspx
 [2]: https://bitbucket.org/Hansen/learningjapanese/changeset/70fa42ad576b3d94d27b2ae00027495f
 [3]: https://bitbucket.org/Hansen/learningjapanese/src/70fa42ad576b3d94d27b2ae00027495f527f06a3/LearningJapanese.Service.Web/Global.asax.cs
 [4]: https://bitbucket.org/Hansen/learningjapanese/src/70fa42ad576b3d94d27b2ae00027495f527f06a3/LearningJapanese.Service/Chat.cs
 [5]: https://bitbucket.org/Hansen/learningjapanese/src/70fa42ad576b3d94d27b2ae00027495f527f06a3/LearningJapanese.Service/LearningJapaneseWeb.cs