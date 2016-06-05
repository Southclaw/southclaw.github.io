---
layout:     post
title:      "MsToString snippet"
date:       2013-08-18 12:02:55
categories: c
---
Here's a quick snippet for generating a string with hours, minutes, seconds and milliseconds in it all from a single milliseconds value. It uses simple format specifiers: 
<!--more-->

  *     "%h" - hours

  *     "%m" - minutes

  *     "%s" - seconds

  *     "%d" - milliseconds


If you entered '8543523' as the value and formatted it as "%1h:%1m:%1s.%1d" the result would be: [![Untitled-1](http://southclawjk.files.wordpress.com/2013/08/untitled-1.png?w=300)](http://southclawjk.files.wordpress.com/2013/08/untitled-1.png) I wanted to do this for a while, mainly for learning and also because my old approach to converting milliseconds to H:M:S.D format strings was a little limited, it had 3 modes which resulted in slightly different formats (H:M:S, H:M:S.D, M:S) but it wasn't enough, I wanted to make a completely customisable method where I could enter format specifiers similar to the "format" function (%d for decimal, %s for string, %f for float, etc...) I also added a padding option, if the hour is 2 and you enter "%h" it will simply be "2" but if you enter "%1h" the result would be "02". It took less time and testing than I thought! However I don't think it's quite as optimised as it could be, the padding options add to the processing time a bit, I expect it's my use of 'str' functions rather than doing it by hand in the function, which may be quicker I'm not sure. Anyhow, here's the function, it executes at around 240-360 times per second (the lowest being all padding options on, the highest being all off) 
    
    
    stock MsToString(millisecond, format[])
    {
    	new
    		tmp[4],
    		result[64],
    		hour,
    		minute,
    		second,
    		format_char,
    		result_lenght,
    		bool:padding,
    		len = strlen(format);
    
    	hour			= (millisecond / (1000 * 60 * 60));
    	minute			= (millisecond % (1000 * 60 * 60)) / (1000 * 60);
    	second			= ((millisecond % (1000 * 60 * 60)) % (1000 * 60)) / 1000;
    	millisecond		= millisecond - (hour * 60 * 60 * 1000) - (minute * 60 * 1000) - (second * 1000);
    
    	while(format_char < len)
    	{
    		if(format[format_char] == '%')
    		{
    			format_char++;
    
    			if(format[format_char] == '1')
    			{
    				padding = true;
    				format_char++;
    			}
    			else
    			{
    				padding = false;
    			}
    
    			switch(format[format_char])
    			{
    				case 'h':
    				{
    					valstr(tmp, hour);
    
    					if(padding)
    					{
    						if(hour < 10)
    							strcat(result, "0");
    					}
    
    					strcat(result, tmp);
    					result_lenght = strlen(result);
    				}
    
    				case 'm':
    				{
    					valstr(tmp, minute);
    
    					if(padding)
    					{
    						if(minute < 10)
    							strcat(result, "0");
    					}
    
    					strcat(result, tmp);
    					result_lenght = strlen(result);
    				}
    
    				case 's':
    				{
    					valstr(tmp, second);
    
    					if(padding)
    					{
    						if(second < 10)
    							strcat(result, "0");
    					}
    
    					strcat(result, tmp);
    					result_lenght = strlen(result);
    				}
    
    				case 'd':
    				{
    					valstr(tmp, millisecond);
    
    					if(padding)
    					{
    						if(millisecond < 10)
    							strcat(result, "00");
    
    						else if(millisecond < 100)
    							strcat(result, "0");
    					}
    
    					strcat(result, tmp);
    					result_lenght = strlen(result);
    				}
    			}
    		}
    		else
    		{
    			result[result_lenght] = format[format_char];
    			result_lenght++;
    		}
    
    		format_char++;
    	}
    
    	return result;
    }
    
