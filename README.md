# Weather_News
Weather information of any area using python

    import pyttsx3 #for speak
    assistant=pyttsx3.init("sapi5") #creation object for speak
    voices=assistant.getProperty('voices') #check voices
    # print(voices)
    assistant.setProperty('voice', voices[1].id) # 1 for female 0 for male
    rate=assistant.getProperty('rate')
    assistant.setProperty('rate',170) #rate of voices

    #speak function for speaking
    def speak(audio):
        assistant.say(audio) #say() method to speak 
        print("")
        assistant.runAndWait() #to run the speech we use runAndWait() All the say() texts won’t be said unless the interpreter encounters runAndWait().
        print("")
    srch=input("Enter city name :")
    import requests #for request data from webpage
    import json #for convert dictionary
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
