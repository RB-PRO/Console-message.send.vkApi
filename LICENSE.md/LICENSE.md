using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Newtonsoft.Json;
using Newtonsoft.Json.Linq;
using xNet;
using VkNet;
using VkNet.Enums.Filters;
using System.Net;
using System.IO;

namespace testVKbot
{
    #pragma warning disable S1118 // Utility classes should not have public constructors
    class Program
    #pragma warning restore S1118 // Utility classes should not have public constructors
    {
        static void Main(string[] args)
        {
            Console.Write("Введите логин: ");
            string log = Console.ReadLine();
            Console.Write("Введите пароль: ");
            string pass = Console.ReadLine();
            var danni = new HttpRequest();
            string response = danni.Get("https://oauth.vk.com/token?grant_type=password&client_id=2274003&client_secret=hHbZxrka2uZ6jB1inYsH&username=" + log + "&password=" + pass).ToString();
            Console.WriteLine(response);
            dynamic json = JObject.Parse(response); //json
            string access_token = json.access_token; //вытаскиваем токен
            string user_id = json.user_id; //вытаскиваем id
            Console.WriteLine("Ваш ID - " + user_id + ". Ваш токен - " + access_token);
            Console.Write("А теперь введите ID человека, кому вы хотите написать сообщение: ");
            string tofiendLine = Console.ReadLine();
            int tofiendInt;
            bool isInt = Int32.TryParse(tofiendLine, out tofiendInt);
            Console.WriteLine(tofiendInt);
            Console.Write("Было бы неплохо написать само сообщение: ");
            string someText = Console.ReadLine();
            // ID моего приложения - 6450572
            danni = new HttpRequest();
            response = danni.Get("https://api.vk.com/method/messages.send?PARAMETERS&user_id=" + tofiendInt + "&message=" + someText + "&access_token=" + access_token + "&v=5.74").ToString();
            Console.WriteLine("федя лох(сосатб)");
            Console.Write("Press any key to continue...");
            Console.ReadKey(true);
        }
    }
}
