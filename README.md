# RingCaptcha for Windows Phone 7.5/8.0
==============================

To install the nuget packages configure a local nuget folder in your developer machine
In your Windows Phone UI project open the context menu and select the option Manage Nuget Packages and search in the configured folder the RingCaptcha.Widget or RingCaptcha.Api package.
Compile your project and add ID_CAP_IDENTITY_DEVICE capability to your Windows Phone UI project 

To use Direct Api
-------------
Instance the apiService

private IRingCaptchaApiService apiService = new RingCaptchaApiService(
	new RingCaptchaConfiguration(
		"YOUR APP KEY", 
		RingCaptchaSource.API, 
		"YOUR DIRECT API KEY"));

This a simple sample of use the apiService

try
{
	var response = await apiService.SendCodeAsync(this.txtPhoneNumber.Text, CaptchaType.VOICE);
	MessageBox.Show(response.Status == Status.SUCCESS.ToString() ? "OK" : response.Message);
}
catch (RingCaptchaInvokeException ex)
{
	MessageBox.Show(ex.Message);
}

To use Widget
-------------

Add the User Control to your pages using the toolbox from Visual Studio or Blend, or add this XAML Code:

NameSpace: xmlns:RingCaptcha="clr-namespace:RingCaptcha.Widget.Controls;assembly=RingCaptcha.Widget"
UserControl: <RingCaptcha:Captcha AppKey="YOUR APP KEY" SecretKey="YOUR SECRET KEY" Domain="YOUR DOMAIN OR APP NAME"/>

To get an advice when the validation is successful subscribe your code to the SucessfulResponseRaised event of the user control instance

<Controls:Captcha x:Name="MyCaptcha" Margin="0" VerticalAlignment="Top" AppKey="YOUR APP KEY" SecretKey="YOUR SECRET KEY" Domain="YOUR DOMAIN OR APP NAME"
SucessfulResponseRaised="MyCaptcha_SucessfulResponseRaised"/>

NOTE: For the right localization you should add to your app the following cultures: pt-BR, es-ES, en-US.


### RingCaptcha. All rights reserved.
