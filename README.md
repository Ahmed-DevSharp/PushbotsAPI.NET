# PushbotsAPI.NET
Pushbots service API using C#

Pushbots API v3 implementation in C# in a simple way.

```C#
    public class PushNotifications
    {
        public async Task<string> Post(string DeviceToken, string title, string message)
        {            
            try
            {
                var url = "https://api.pushbots.com/3/push/transactional";

                var con = "{ " +
                "\"topic\":\"Contoraz\" ," +
                "\"badge\": \"0\" , " +
                "\"message\": {" +
                "\"title\": \"" + title + "\"," +
                "\"body\":\"" + message + "\"," +
                "\"payload\": {} " +
                "}, " +
                "\"platform\":1, " +
                "\"recipients\":{ " +
                "\"tokens\":" +
                "[\"" + DeviceToken + "\"] " +
                "}" +
                "}";
            
                var httpContent = new StringContent(con, Encoding.UTF8, "application/json");

                HttpClient client = new HttpClient();

                client.DefaultRequestHeaders.Add("x-pushbots-appid", "[Pushbots App Id]");
                client.DefaultRequestHeaders.Add("x-pushbots-secret", "[Pushbots App Secret]");

                HttpResponseMessage response = await client.PostAsync(url , httpContent);

                return response.ToString();
            }
            catch (Exception ex)
            {
                return ex.Message;
            }
        }
    }
```
