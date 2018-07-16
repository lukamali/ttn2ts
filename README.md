# LoRaWAN ttn2ts Proxy
TheThingsNetwork to ThingSpeak Proxy

## Arduino/Node Payload Data Encoder

Example for two float variables:

> // Define variables
>
> Byte Data[4];
>
> int temperature = 22.00;
>
> int humidity = 45.00;
>
>
> // Translate float value to int 16 bit (*100 get rid of the decimale point)
>
> int16_t temperature100 = (int16_t)(temperature * 100);
>
> int16_t humidity100 = (int16_t)(humidity * 100);
>
>
> // Shift bits and store the value in Bytes
>
> Data[0] = temperature100 >> 8;
>
> Data[1] = temperature100 & 0xFF;
>
> Data[2] = humidity100 >> 8;
>
> Data[3] = humidity100 & 0xFF;


## TTN Payload Data Decoder
Go to "TTN -> Applications -> MY_APPLICATION_NAME -> Payload Formats -> decoder"

Add the following code (example for two float variables):

> function Decoder(bytes) {
>
>  var temperature100 = (bytes[0] << 8) | bytes[1];
>
>  var humidity100 = (bytes[2] << 8) | bytes[3];
>
>  return { temperature: temperature100 / 100.0, humidity: humidity100 / 100.0 };
>
> }

Click **Save payload functions**


## TTN HTTP Integration

Go to "TTN -> Applications -> MY_APPLICATION_NAME -> Integrations"

Add integration: **HTTP Integration**

Select Access Key: **default key**

Add URL (and use your TS API Key and TTN field names): 
> http://mali.si/ttn2ts/?api_key=MY_TS_WRITE_API_KEY&field1=temperature&field2=humidity

_Proxy supports up to 8 field parameters._

Click **Save**
