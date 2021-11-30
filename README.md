# Weather_News
Weather information of any area using python

    srch=srch.replace("jarvis",'')
    srch=srch.replace("weather","")
    srch=srch.replace("of",'')
    srch=srch.replace('news','')
    srch=srch.replace('report','')
    srch=srch.replace("tell me","")
    srch=srch.replace("information",'')
    #weather api
    url='http://api.openweathermap.org/data/2.5/weather?q=+'+srch+'&appid=067fda8d35b3c88f50a2be0f2945f1f5'
    data=requests.get(url).text #get all the information as string
    data=json.loads(data) #convert string into dict
    # print(data)
    if(data['cod']==404): #if city name not valid
        speak("invalid city name..Please check your city name sir..")
    else:
        #get all the information
        temp_City=data['main']['temp']-273.15 #get temperature in k ...so -273.15
        temp_City=round(temp_City,2) #round figure
        temp=str(temp_City)
        weather_des=data["weather"][0]["description"] 
        hmdt=data['main']['humidity']
        speed_air=data["wind"]["speed"]
        #for better broadcast
        weather_tell="Current weather is"+weather_des
        hmdt_tell="Current humidity is"+str(hmdt)+"percentage"
        speed_tell="Current air speed is "+str(speed_air)+"kilometers per hour"
        tell="Current Temperature is"+temp+"degree celcius"
        report="weather report of "+srch+"is broadcast ...listen carefully"
        #speak all the information
        speak(report)
        speak(weather_tell)
        speak(tell)
        speak(hmdt_tell)
        speak(speed_tell)
