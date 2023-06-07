---
layout: post
title: Post on twitter/kwippy using .NET
date: '2009-03-03T14:42:58+05:30'
tags:
- cool
- kwippy
- micro
- net
- platform
- post
- twitter
tumblr_url: http://www.desinerd.com/post/150535099948/post-on-twitterkwippy-using-net
---
                                                                                                                                             




using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO; 
using System.Net; 
using System.Web;
 
namespace ConsoleApplication1
{
 class Program
 {
 static void Main(string[] args)
 {
 System.Net.ServicePointManager.Expect100Continue = false;
 Uri address = new Uri(“http://twitter.com/statuses/update.json”);
 // Create the web request 
 HttpWebRequest request = WebRequest.Create(address) as HttpWebRequest;
 request.Method = “POST”; 
 request.ContentType = “application/x-www-form-urlencoded”;
 request.Credentials = new NetworkCredential(“username”, “password”);
 StringBuilder data = new StringBuilder(); 
 data.Append(“status=from%20.net”);
 // Create a byte array of the data we want to send 
 byte[] byteData = UTF8Encoding.UTF8.GetBytes(data.ToString()); 
 // Set the content length in the request headers 
 request.ContentLength = byteData.Length;
 using (Stream postStream = request.GetRequestStream()) 
 { 
 postStream.Write(byteData, 0, byteData.Length); 
 } 
 using (HttpWebResponse response = request.GetResponse() as HttpWebResponse) 
 { 
 // Get the response stream 
 StreamReader reader = new StreamReader(response.GetResponseStream());
 // Console application output 
 Console.WriteLine(reader.ReadToEnd()); 
 }
 }
 }
}

Code to post on twitter and kwippy using this simple C# program :). Njoi.
