1. Let’s begin our exploration of HTTP by downloading a very simple HTML file - one that is very short and contains no embedded objects. Do the following:
1. Start up your web browser.
2. Start the Wireshark packet sniffer, as described in the Introductory lab (but don’t yet begin packet capture). Enter “http” (just the letters, not the quotation marks) in the display-filter-specification window, so that only captured HTTP messages will be displayed later in the packet-listing window. (We’re only interested in the HTTP protocol here, and don’t want to see the clutter of all captured packets).
3. Wait more than one minute (we’ll see why shortly), and then begin Wireshark packet capture.
4. Enter the following into your browser
http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file1.html
Your browser should display a very simple, one-line HTML file.
5. Stop Wireshark packet capture.

## 1. HTTP GET and response messages

![image](https://github.com/user-attachments/assets/c2b434df-c6d0-4719-8db9-8744920e6d2d)
This is the webpage of the given HTTP website.

### _1. Is your browser running HTTP version 1.0 or 1.1? What version of HTTP is the server running?_

![image](https://github.com/user-attachments/assets/eb95e16b-8964-4cf5-8eb2-79b2d386d468)
By analysing the HTTP request, we can identify the version of HTTP used on our local system. My browser is running HTTP version 1.1.

![image](https://github.com/user-attachments/assets/7157da01-1226-48cc-a0c9-198b2c576024)
By analysing the HTTP response, we can identify the version of HTTP used on the server side. The server is running HTTP version 1.1.

### _2. What languages (if any) do your browser indicate that it can accept to the server?_

![image](https://github.com/user-attachments/assets/e973946f-6222-467a-9d47-212cd65919a6)
By analysing the HTTP request, we can identify the encoding and language that my browser can accept from the server.
- Accept-Encoding: gzip, deflate\r\n
- Accept-Language: en-US,en;q=0.9\r\n
- My browser accepts English (United States) responses.

### _3. What is the IP address of your computer? What is the IP address of the gaia.cs.umass.edu server?_

![image](https://github.com/user-attachments/assets/bb3a7387-39e1-4945-a360-112c249f2928)
By analysing either the request or the response packet, under the network layer – Internet protocol, we can find the source and destination IP addresses.
- IP address of my computer is 10.11.132.117.
- IP address of the gaia.cs.unmass.edu server is 128.119.245.12

### _4. What is the status code returned from the server to your browser?_

![image](https://github.com/user-attachments/assets/401d6a27-121a-4823-8195-b8cf6d57a4d9)
Under application layer where HTTP response is unwrapped, we can see the status code and its descriptor. The status code of the response is 200 [OK].

### _5. When was the HTML file that you are retrieving last modified at the server?_

![image](https://github.com/user-attachments/assets/09941265-81da-485a-a401-bd92e579f5bf)
The if-modified-since is a GET request header. To determine when a HTML file was last modified, we need to identify the if-modified-since header under HTTP. There is no if-modified-since header in the request packet.

### _6. How many bytes of content are being returned to your browser?_

![image](https://github.com/user-attachments/assets/0cdb3483-a631-4aa2-ba7c-79f4957eec1d)
128 bytes of content are returned from server to the browser.

### _7. By inspecting the raw data in the packet content window, do you see any headers within the data that are not displayed in the packet-listing window? If so, name one._

All the headers in the raw data are also displayed in the packet-listing window.

## 2. IF-MODIFIED-SINCE

1. Start up your web browser, and make sure your browser’s cache is cleared, as discussed above.
2. Start up the Wireshark packet sniffer
3. Enter the following URL into your browser: http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file2.html
4. Your browser should display a very simple five-line HTML file.
5. Quickly enter the same URL into your browser again (or simply select the refresh button on your browser)
6. Stop Wireshark packet capture and enter “http” in the display-filter-specification window, so that only captured HTTP messages will be displayed later in the packet-listing window.

![image](https://github.com/user-attachments/assets/3fe73335-6755-425d-af97-f55df6fe50f1)

### _8. Inspect the contents of the first HTTP GET request from your browser to the server. Do you see an “IF-MODIFIED-SINCE” line in the HTTP GET?_

![image](https://github.com/user-attachments/assets/a82a01c6-4664-4b9d-9f92-c5c14778dd36)
There is no if-modified-since header in the HTTP GET request.

### _9. Inspect the contents of the server response. Did the server explicitly return the contents of the file? How can you tell?_

![image](https://github.com/user-attachments/assets/388c1a88-0de4-48a3-bcd5-fd1b5f5c5fc1)
We can see that the HTML code of the webpage is also displayed along with the headers in the packet-listing window. The server has explicitly returned the contents of the file.

### _10. Now inspect the contents of the second HTTP GET request from your browser to the server. Do you see an “IF-MODIFIED-SINCE:” line in the HTTP GET? What information follows the “IF-MODIFIED-SINCE:” header?_

![image](https://github.com/user-attachments/assets/794780b5-5c9b-40eb-b8ab-d85ac17ce655)
We can now see the if-modified-since header in the second GET request. If-Modified-Since: Tue, 06 Aug 2024 05:59:01 GMT\r\n

### _11. What is the HTTP status code and phrase returned from the server in response to this second HTTP GET? Did the server explicitly return the file’s contents? Explain._

![image](https://github.com/user-attachments/assets/e53ed14d-c87c-4804-9c49-d5d98ffbd0aa)
Status code and descriptor for the second response is 304 [Not Modified]. This time, the file did not explicitly return the contents of the file.

## 3. Bill of Rights

1. Start up your web browser, and make sure your browser’s cache is cleared, as discussed above.
2. Start up the Wireshark packet sniffer
3. Enter the following URL into your browser: http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file3.html
4. Your browser should display the rather lengthy US Bill of Rights.
5. Stop Wireshark packet capture and enter “http” in the display-filter-specification window, so that only captured HTTP messages will be displayed.

![image](https://github.com/user-attachments/assets/31040b16-4d66-4e28-a9fc-39c3f3c8eec7)

### _12. How many HTTP GET request messages did your browser send? Which packet number in the trace contains the GET message for the Bill of Rights?_

![image](https://github.com/user-attachments/assets/c2ee5421-b65a-4e0b-b052-81917cb2a06f)

My browser sent two HTTP GET requests to the server. One request for the file contained in the server and one request for the favicon icon for the webpage. Packet number 6939 contains the GET message for the Bill of Rights.

### _13. Which packet number in the trace contains the status code and phrase associated with the response to the HTTP GET request?_

![image](https://github.com/user-attachments/assets/cff49d2a-2c5f-4b21-ac13-925c28c0bb0e)

Packet number 7257 contains the HTTP response – Bill of Rights.

### _14. What is the status code and phrase in the response?_

![image](https://github.com/user-attachments/assets/e317a8bf-448a-4db9-8d8e-b460f916a1d9)
The status code and descriptor for the corresponding response is 200 [OK].

### _15. How many data-containing TCP segments were needed to carry the single HTTP response and the text of the Bill of Rights?_

![image](https://github.com/user-attachments/assets/00bfd12a-bf6b-4f53-af93-386f588c8b6e)
Four TCP segments were needed to carry the single HTTP response containing the Bill of Rights.

## 4. HTTP Authentication

Finally, let’s try visiting a website that is password-protected and examining the sequence of HTTP messages exchanged for such a site. The URL http://gaia.cs.umass.edu/wireshark-labs/protected_pages/HTTP-wireshark-file5.html is password protected. The username is “Wireshark-students” (without the quotes), and the password is “network” (again, without the quotes). So, let’s access this “secure” password-protected site.

1. Make sure your browser’s cache is cleared, as discussed above, and close your browser. Then, start up your browser
2. Start up the Wireshark packet sniffer
3. Enter the following URL into your browser http://gaia.cs.umass.edu/wireshark-labs/protected_pages/HTTP-wiresharkfile5.html Type the requested username and password into the pop-up box.
4. Stop Wireshark packet capture and enter “http” in the display-filter-specification window, so that only captured HTTP messages will be displayed later in the packet-listing window.

![image](https://github.com/user-attachments/assets/5f2d72b7-82df-4182-b0d1-595f894673ca)

![image](https://github.com/user-attachments/assets/81c7ceda-7c3e-4b93-a980-e712bc021ad5)

### _16. What is the server’s response (status code and phrase) in response to the initial HTTP GET message from your browser?_

![image](https://github.com/user-attachments/assets/a7da6d82-87b1-4cbc-8636-7b7589cd57a0)
To the initial GET request, the server responded with a 401 [Unauthorised] status code.

### _17. When your browser sends the HTTP GET message for the second time, what new field is included in the HTTP GET message?_

![image](https://github.com/user-attachments/assets/1b236ffb-2860-4897-bf58-2dd59e15b6a0)
Authorization field is included in the second HTTP GET request. It contained the username and password credentials being sent to the server.





