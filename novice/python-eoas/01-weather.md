---
layout: lesson
root: ../..
---

# EOAS Python - Reading and Exploring CSV Data


<div>
<h2 id="learning-goals">Learning Goals</h2>
<ul>
<li>Read CSV data from files into NumPy data structures, using <a href="http://pandas.pydata.org/">pandas</a></li>
<li>Use list boolean slices to select data</li>
</ul>
</div>


<div>
<h2 id="reading-csv-data-files">Reading CSV Data Files</h2>
</div>


<div class="in">
<pre>import numpy as np
import pandas as pd</pre>
</div>


<div>
<p>Earlier we used numpy.loadtxt to read our csv. Now we will use the <a href="http://pandas.pydata.org/">pandas</a> data analysis library, that handles data better; in particular, headers in our files.</p>
<p>However even with panda if we try the simplest possible thing:</p>
<pre class="sourceCode python"><code class="sourceCode python">data = pd.read_csv(<span class="st">&#39;eng-hourly-08012013-08312013.csv&#39;</span>)</code></pre>
<p>we get a dismaying number of errors.</p>
<p>Let's take a look at the data. You can use shell commands within notebook cells by prefixing them with <code>!</code>.</p>
</div>


<div class="in">
<pre>!head eng-hourly-08012013-08312013.csv</pre>
</div>

<div class="out">
<pre>&#34;Station Name&#34;,&#34;VANCOUVER INTL A&#34;
&#34;Province&#34;,&#34;BRITISH COLUMBIA&#34;
&#34;Latitude&#34;,&#34;49.19&#34;
&#34;Longitude&#34;,&#34;-123.18&#34;
&#34;Elevation&#34;,&#34;4.30&#34;
&#34;Climate Identifier&#34;,&#34;1108395&#34;
&#34;WMO Identifier&#34;,&#34;71892&#34;
&#34;TC Identifier&#34;,&#34;YVR&#34;
&#34;All times are specified in Local Standard Time (LST). Add 1 hour to adjust for Daylight Saving Time where and when it is observed.&#34;

</pre>
</div>


<div class="in">
<pre>!head -20 eng-hourly-08012013-08312013.csv</pre>
</div>

<div class="out">
<pre>&#34;Station Name&#34;,&#34;VANCOUVER INTL A&#34;
&#34;Province&#34;,&#34;BRITISH COLUMBIA&#34;
&#34;Latitude&#34;,&#34;49.19&#34;
&#34;Longitude&#34;,&#34;-123.18&#34;
&#34;Elevation&#34;,&#34;4.30&#34;
&#34;Climate Identifier&#34;,&#34;1108395&#34;
&#34;WMO Identifier&#34;,&#34;71892&#34;
&#34;TC Identifier&#34;,&#34;YVR&#34;
&#34;All times are specified in Local Standard Time (LST). Add 1 hour to adjust for Daylight Saving Time where and when it is observed.&#34;

&#34;Legend&#34;
&#34;M&#34;,&#34;Missing&#34;
&#34;E&#34;,&#34;Estimated&#34;
&#34;NA&#34;,&#34;Not Available&#34;
&#34;**&#34;,&#34;Partner data that is not subject to review by the National Climate Archives&#34;

&#34;Date/Time&#34;,&#34;Year&#34;,&#34;Month&#34;,&#34;Day&#34;,&#34;Time&#34;,&#34;Data Quality&#34;,&#34;Temp (�C)&#34;,&#34;Temp Flag&#34;,&#34;Dew Point Temp (�C)&#34;,&#34;Dew Point Temp Flag&#34;,&#34;Rel Hum (%)&#34;,&#34;Rel Hum Flag&#34;,&#34;Wind Dir (10s deg)&#34;,&#34;Wind Dir Flag&#34;,&#34;Wind Spd (km/h)&#34;,&#34;Wind Spd Flag&#34;,&#34;Visibility (km)&#34;,&#34;Visibility Flag&#34;,&#34;Stn Press (kPa)&#34;,&#34;Stn Press Flag&#34;,&#34;Hmdx&#34;,&#34;Hmdx Flag&#34;,&#34;Wind Chill&#34;,&#34;Wind Chill Flag&#34;,&#34;Weather&#34;
&#34;2013-08-01 00:00&#34;,&#34;2013&#34;,&#34;08&#34;,&#34;01&#34;,&#34;00:00&#34;,&#34;**&#34;,&#34;18.7&#34;,&#34;&#34;,&#34;14.6&#34;,&#34;&#34;,&#34;77&#34;,&#34;&#34;,&#34;13&#34;,&#34;&#34;,&#34;3&#34;,&#34;&#34;,&#34;32.2&#34;,&#34;&#34;,&#34;101.60&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;Rain&#34;
&#34;2013-08-01 01:00&#34;,&#34;2013&#34;,&#34;08&#34;,&#34;01&#34;,&#34;01:00&#34;,&#34;**&#34;,&#34;18.4&#34;,&#34;&#34;,&#34;15.1&#34;,&#34;&#34;,&#34;81&#34;,&#34;&#34;,&#34;1&#34;,&#34;&#34;,&#34;5&#34;,&#34;&#34;,&#34;32.2&#34;,&#34;&#34;,&#34;101.57&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;Cloudy&#34;
&#34;2013-08-01 02:00&#34;,&#34;2013&#34;,&#34;08&#34;,&#34;01&#34;,&#34;02:00&#34;,&#34;**&#34;,&#34;17.8&#34;,&#34;&#34;,&#34;16.0&#34;,&#34;&#34;,&#34;89&#34;,&#34;&#34;,&#34;18&#34;,&#34;&#34;,&#34;9&#34;,&#34;&#34;,&#34;24.1&#34;,&#34;&#34;,&#34;101.57&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;Rain&#34;
</pre>
</div>


<div class="in">
<pre>!tail eng-hourly-08012013-08312013.csv</pre>
</div>

<div class="out">
<pre>&#34;2013-08-31 14:00&#34;,&#34;2013&#34;,&#34;08&#34;,&#34;31&#34;,&#34;14:00&#34;,&#34;**&#34;,&#34;19.4&#34;,&#34;&#34;,&#34;16.3&#34;,&#34;&#34;,&#34;82&#34;,&#34;&#34;,&#34;30&#34;,&#34;&#34;,&#34;19&#34;,&#34;&#34;,&#34;48.3&#34;,&#34;&#34;,&#34;101.43&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;NA&#34;
&#34;2013-08-31 15:00&#34;,&#34;2013&#34;,&#34;08&#34;,&#34;31&#34;,&#34;15:00&#34;,&#34;**&#34;,&#34;19.3&#34;,&#34;&#34;,&#34;16.0&#34;,&#34;&#34;,&#34;81&#34;,&#34;&#34;,&#34;31&#34;,&#34;&#34;,&#34;22&#34;,&#34;&#34;,&#34;48.3&#34;,&#34;&#34;,&#34;101.32&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;NA&#34;
&#34;2013-08-31 16:00&#34;,&#34;2013&#34;,&#34;08&#34;,&#34;31&#34;,&#34;16:00&#34;,&#34;**&#34;,&#34;19.6&#34;,&#34;&#34;,&#34;16.1&#34;,&#34;&#34;,&#34;80&#34;,&#34;&#34;,&#34;30&#34;,&#34;&#34;,&#34;18&#34;,&#34;&#34;,&#34;48.3&#34;,&#34;&#34;,&#34;101.23&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;Mainly Clear&#34;
&#34;2013-08-31 17:00&#34;,&#34;2013&#34;,&#34;08&#34;,&#34;31&#34;,&#34;17:00&#34;,&#34;**&#34;,&#34;19.5&#34;,&#34;&#34;,&#34;16.0&#34;,&#34;&#34;,&#34;80&#34;,&#34;&#34;,&#34;30&#34;,&#34;&#34;,&#34;18&#34;,&#34;&#34;,&#34;48.3&#34;,&#34;&#34;,&#34;101.16&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;NA&#34;
&#34;2013-08-31 18:00&#34;,&#34;2013&#34;,&#34;08&#34;,&#34;31&#34;,&#34;18:00&#34;,&#34;**&#34;,&#34;18.7&#34;,&#34;&#34;,&#34;16.0&#34;,&#34;&#34;,&#34;84&#34;,&#34;&#34;,&#34;30&#34;,&#34;&#34;,&#34;16&#34;,&#34;&#34;,&#34;48.3&#34;,&#34;&#34;,&#34;101.08&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;NA&#34;
&#34;2013-08-31 19:00&#34;,&#34;2013&#34;,&#34;08&#34;,&#34;31&#34;,&#34;19:00&#34;,&#34;**&#34;,&#34;17.6&#34;,&#34;&#34;,&#34;16.1&#34;,&#34;&#34;,&#34;91&#34;,&#34;&#34;,&#34;30&#34;,&#34;&#34;,&#34;13&#34;,&#34;&#34;,&#34;48.3&#34;,&#34;&#34;,&#34;101.06&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;Mainly Clear&#34;
&#34;2013-08-31 20:00&#34;,&#34;2013&#34;,&#34;08&#34;,&#34;31&#34;,&#34;20:00&#34;,&#34;**&#34;,&#34;17.4&#34;,&#34;&#34;,&#34;15.8&#34;,&#34;&#34;,&#34;90&#34;,&#34;&#34;,&#34;29&#34;,&#34;&#34;,&#34;12&#34;,&#34;&#34;,&#34;32.2&#34;,&#34;&#34;,&#34;101.03&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;NA&#34;
&#34;2013-08-31 21:00&#34;,&#34;2013&#34;,&#34;08&#34;,&#34;31&#34;,&#34;21:00&#34;,&#34;**&#34;,&#34;16.7&#34;,&#34;&#34;,&#34;15.6&#34;,&#34;&#34;,&#34;93&#34;,&#34;&#34;,&#34;30&#34;,&#34;&#34;,&#34;9&#34;,&#34;&#34;,&#34;32.2&#34;,&#34;&#34;,&#34;101.00&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;NA&#34;
&#34;2013-08-31 22:00&#34;,&#34;2013&#34;,&#34;08&#34;,&#34;31&#34;,&#34;22:00&#34;,&#34;**&#34;,&#34;17.1&#34;,&#34;&#34;,&#34;16.1&#34;,&#34;&#34;,&#34;94&#34;,&#34;&#34;,&#34;32&#34;,&#34;&#34;,&#34;13&#34;,&#34;&#34;,&#34;32.2&#34;,&#34;&#34;,&#34;100.99&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;Mainly Clear&#34;
&#34;2013-08-31 23:00&#34;,&#34;2013&#34;,&#34;08&#34;,&#34;31&#34;,&#34;23:00&#34;,&#34;**&#34;,&#34;15.5&#34;,&#34;&#34;,&#34;14.6&#34;,&#34;&#34;,&#34;94&#34;,&#34;&#34;,&#34;34&#34;,&#34;&#34;,&#34;10&#34;,&#34;&#34;,&#34;32.2&#34;,&#34;&#34;,&#34;101.02&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;NA&#34;
</pre>
</div>


<div>
<p>So, we have several lines of header data, with a couple of empty lines thrown in, a line of column names, and then line after line of data. The data values appear to be all <code>&quot;&quot;</code> quoted strings delimited by commas. Comma is assumed delimiter by pandas.read_csv.</p>
<p>We will just throw away all of the non-data lines. Counting them manually we find that there are 17 total, but we'll keep the column names.</p>
</div>


<div class="in">
<pre>data = pd.read_csv(&#39;eng-hourly-08012013-08312013.csv&#39;, skiprows=16)
print data[0:4]</pre>
</div>

<div class="out">
<pre>          Date/Time  Year  Month  Day   Time Data Quality  Temp (°C)  \
0  2013-08-01 00:00  2013      8    1  00:00           **       18.7   
1  2013-08-01 01:00  2013      8    1  01:00           **       18.4   
2  2013-08-01 02:00  2013      8    1  02:00           **       17.8   
3  2013-08-01 03:00  2013      8    1  03:00           **       17.2   

   Temp Flag  Dew Point Temp (°C)  Dew Point Temp Flag         ...           \
0        NaN                 14.6                  NaN         ...            
1        NaN                 15.1                  NaN         ...            
2        NaN                 16.0                  NaN         ...            
3        NaN                 15.6                  NaN         ...            

   Wind Spd Flag  Visibility (km)  Visibility Flag  Stn Press (kPa)  \
0            NaN             32.2              NaN           101.60   
1            NaN             32.2              NaN           101.57   
2            NaN             24.1              NaN           101.57   
3            NaN             32.2              NaN           101.57   

   Stn Press Flag  Hmdx  Hmdx Flag  Wind Chill  Wind Chill Flag  Weather  
0             NaN   NaN        NaN         NaN              NaN     Rain  
1             NaN   NaN        NaN         NaN              NaN   Cloudy  
2             NaN   NaN        NaN         NaN              NaN     Rain  
3             NaN   NaN        NaN         NaN              NaN      NaN  

[4 rows x 25 columns]
</pre>
</div>


<div class="in">
<pre>print data.tail(1)</pre>
</div>

<div class="out">
<pre>            Date/Time  Year  Month  Day   Time Data Quality  Temp (�C)  \
743  2013-08-31 23:00  2013      8   31  23:00           **       15.5   

     Temp Flag  Dew Point Temp (�C)  Dew Point Temp Flag         ...           \
743        NaN                 14.6                  NaN         ...            

     Wind Spd Flag  Visibility (km)  Visibility Flag  Stn Press (kPa)  \
743            NaN             32.2              NaN           101.02   

     Stn Press Flag  Hmdx  Hmdx Flag  Wind Chill  Wind Chill Flag  Weather  
743             NaN   NaN        NaN         NaN              NaN      NaN  

[1 rows x 25 columns]
</pre>
</div>


<div class="in">
<pre>!tail -1 eng-hourly-08012013-08312013.csv</pre>
</div>

<div class="out">
<pre>&#34;2013-08-31 23:00&#34;,&#34;2013&#34;,&#34;08&#34;,&#34;31&#34;,&#34;23:00&#34;,&#34;**&#34;,&#34;15.5&#34;,&#34;&#34;,&#34;14.6&#34;,&#34;&#34;,&#34;94&#34;,&#34;&#34;,&#34;34&#34;,&#34;&#34;,&#34;10&#34;,&#34;&#34;,&#34;32.2&#34;,&#34;&#34;,&#34;101.02&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;&#34;,&#34;NA&#34;
</pre>
</div>


<div>
<p>That looks like progress and looks like what we expect.</p>
<p>One remaining issue</p>
<p>The degree symbol in the data file has been mangled. This is because pandas is not using the correct encoding. From trial and error we find that EC is using Windows encoding : ISO-8859-1</p>
</div>


<div class="in">
<pre>data = pd.read_csv(&#39;eng-hourly-08012013-08312013.csv&#39;, skiprows=16, encoding=&#34;ISO-8859-1&#34;)
print data.columns</pre>
</div>

<div class="out">
<pre>Index([u&#39;Date/Time&#39;, u&#39;Year&#39;, u&#39;Month&#39;, u&#39;Day&#39;, u&#39;Time&#39;, u&#39;Data Quality&#39;, u&#39;Temp (°C)&#39;, u&#39;Temp Flag&#39;, u&#39;Dew Point Temp (°C)&#39;, u&#39;Dew Point Temp Flag&#39;, u&#39;Rel Hum (%)&#39;, u&#39;Rel Hum Flag&#39;, u&#39;Wind Dir (10s deg)&#39;, u&#39;Wind Dir Flag&#39;, u&#39;Wind Spd (km/h)&#39;, u&#39;Wind Spd Flag&#39;, u&#39;Visibility (km)&#39;, u&#39;Visibility Flag&#39;, u&#39;Stn Press (kPa)&#39;, u&#39;Stn Press Flag&#39;, u&#39;Hmdx&#39;, u&#39;Hmdx Flag&#39;, u&#39;Wind Chill&#39;, u&#39;Wind Chill Flag&#39;, u&#39;Weather&#39;], dtype=&#39;object&#39;)
</pre>
</div>


<div>
<h2 id="descriptive-statistics">Descriptive Statistics</h2>
<p>Now we can use array methods to do some basic analysis of the August 2013 weather. Let's look at temperatures:</p>
</div>


<div class="in">
<pre>temps = data[u&#39;Temp (°C)&#39;]
print &#39;max:&#39;, temps.max(), &#39;on&#39;, data[&#39;Date/Time&#39;][temps.argmax()]
print &#39;min:&#39;, temps.min(), &#39;on&#39;, data[&#39;Date/Time&#39;][temps.argmin()]
print &#39;mean:&#39;, temps.mean()
print &#39;std dev:&#39;, temps.std()</pre>
</div>

<div class="out">
<pre>max: 24.6 on 2013-08-10 15:00
min: 12.5 on 2013-08-31 06:00
mean: 18.4383064516
std dev: 2.67368872431
</pre>
</div>


<div>
<p>Note that we need to include the u infront of Temp to warn python that this string includes unicode. I got the degree symbol by copying and pasting.</p>
<p>Now let's use Boolean slicing to dig down to the day level in our data. Let's get the maximum temperature each day, and the time when it occurred.</p>
</div>


<div class="in">
<pre>temps = data[u&#39;Temp (°C)&#39;]
for day in range(1, 32):
    mask = data[&#39;Day&#39;]==day
    max_temp = temps[mask].max()
    date = data[mask][&#39;Date/Time&#39;][temps[mask].argmax()][:11]
    hour = data[mask][&#39;Time&#39;][temps[mask].argmax()]    
    print &#39;max temperature on&#39;,date, &#39;was&#39;, max_temp, &#39;at&#39;, hour</pre>
</div>

<div class="out">
<pre>max temperature on 2013-08-01  was 21.2 at 14:00
max temperature on 2013-08-02  was 17.6 at 16:00
max temperature on 2013-08-03  was 20.2 at 17:00
max temperature on 2013-08-04  was 22.3 at 15:00
max temperature on 2013-08-05  was 22.7 at 14:00
max temperature on 2013-08-06  was 23.6 at 17:00
max temperature on 2013-08-07  was 24.5 at 17:00
max temperature on 2013-08-08  was 23.7 at 17:00
max temperature on 2013-08-09  was 23.9 at 14:00
max temperature on 2013-08-10  was 24.6 at 15:00
max temperature on 2013-08-11  was 21.1 at 14:00
max temperature on 2013-08-12  was 23.0 at 13:00
max temperature on 2013-08-13  was 22.6 at 18:00
max temperature on 2013-08-14  was 23.4 at 11:00
max temperature on 2013-08-15  was 21.8 at 10:00
max temperature on 2013-08-16  was 23.5 at 13:00
max temperature on 2013-08-17  was 23.8 at 16:00
max temperature on 2013-08-18  was 22.0 at 17:00
max temperature on 2013-08-19  was 22.4 at 16:00
max temperature on 2013-08-20  was 21.4 at 16:00
max temperature on 2013-08-21  was 22.1 at 14:00
max temperature on 2013-08-22  was 24.2 at 15:00
max temperature on 2013-08-23  was 22.1 at 14:00
max temperature on 2013-08-24  was 20.9 at 13:00
max temperature on 2013-08-25  was 22.0 at 16:00
max temperature on 2013-08-26  was 22.3 at 14:00
max temperature on 2013-08-27  was 22.0 at 14:00
max temperature on 2013-08-28  was 21.8 at 16:00
max temperature on 2013-08-29  was 20.5 at 15:00
max temperature on 2013-08-30  was 21.6 at 16:00
max temperature on 2013-08-31  was 19.6 at 16:00
</pre>
</div>


<div>
<p><strong>Exercise:</strong> Plot the daily maximum temperature.</p>
</div>


<div>
<p>But what if you want to look at lots of files. Can we automate downloading of the files? Yes! 1) You can use subprocess to go out to shell and run curl or wget<br />2) You can use the requests library<br />3) You can use the url library</p>
</div>


<div>
<p>It takes some digging around, but it turns out that sending an HTTP GET request to:</p>
<p>http://climate.weather.gc.ca/climateData/bulkdata_e.html?timeframe=1&amp;stationID=51442&amp;Year=2013&amp;Month=8&amp;Day=1&amp;format=csv</p>
<p>will return the hourly data CSV file for YVR that we all downloaded earlier.</p>
<p>Note: The program that accepts that URL and processes it to return the data is very picky about capitalization. That's not good design, but it's what we have to live with.</p>
<p>We can write that URL more readably in Python by separating it into a string for the URL of the page, and a dictionary containing the keys and values in the query part. Then we can use requests.get() function to get the content at that URL:</p>
</div>


<div class="in">
<pre>import requests
url = &#39;http://climate.weather.gc.ca/climateData/bulkdata_e.html&#39;
params = {
    &#39;timeframe&#39;: 1,
    &#39;stationID&#39;: 51442,
    &#39;Year&#39;: 2013,
    &#39;Month&#39;: 7,
    &#39;Day&#39;: 1,
    &#39;format&#39;: &#39;csv&#39;,
}
response = requests.get(url, params=params)</pre>
</div>


<div>
<p>The response object that we get back has a variety of properties and methods. We can look at the response headers:</p>
</div>


<div class="in">
<pre>response.headers</pre>
</div>

<div class="out">
<pre>{&#39;content-disposition&#39;: &#39;attachment; filename=&#34;eng-hourly-07012013-07312013.csv&#34;&#39;, &#39;content-transfer-encoding&#39;: &#39;binary&#39;, &#39;set-cookie&#39;: &#39;jsenabled=0; expires=Mon, 15-Sep-2014 02:50:46 GMT; path=/&#39;, &#39;accept-ranges&#39;: &#39;bytes&#39;, &#39;expires&#39;: &#39;Mon, 26 Jul 1997 05:00:00 GMT&#39;, &#39;keep-alive&#39;: &#39;timeout=3, max=100&#39;, &#39;server&#39;: &#39;Apache&#39;, &#39;transfer-encoding&#39;: &#39;chunked&#39;, &#39;connection&#39;: &#39;Keep-Alive&#39;, &#39;pragma&#39;: &#39;public&#39;, &#39;cache-control&#39;: &#39;private&#39;, &#39;date&#39;: &#39;Mon, 15 Sep 2014 01:50:46 GMT&#39;, &#39;content-type&#39;: &#39;application/force-download&#39;}
None
</pre>
</div>


<div>
<p>to see that:</p>
<p>'content-disposition': 'attachment; filename=&quot;eng-hourly-08012013-08312013.csv&quot;'</p>
<p>which is why our browsers download the file with the name that they do, or offer to open it for us in an appropriate application. We can also see that:</p>
<p>'content-type': 'text/csv'</p>
<p>confirms that the server is sending us CSV data.</p>
<p>Now we have a bit of a library mis-match. Response produces a response object that has a bunch of neat properties BUT pandas wants to read a file. So we use the python library StringIO to produce a fakefile from the response content.</p>
</div>


<div class="in">
<pre>from StringIO import StringIO
fakefile = StringIO(response.content)
datajul = pd.read_csv(fakefile, skiprows=16, encoding = &#34;ISO-8859-1&#34;)

print datajul.head(2)</pre>
</div>

<div class="out">
<pre>          Date/Time  Year  Month  Day   Time Data Quality  Temp (°C)  \
0  2013-07-01 00:00  2013      7    1  00:00           **       19.6   
1  2013-07-01 01:00  2013      7    1  01:00           **       18.7   

   Temp Flag  Dew Point Temp (°C) Dew Point Temp Flag         ...          \
0        NaN                 17.8                 NaN         ...           
1        NaN                 16.7                 NaN         ...           

   Wind Spd Flag Visibility (km)  Visibility Flag Stn Press (kPa)  \
0            NaN            32.2              NaN          101.22   
1            NaN            32.2              NaN          101.26   

   Stn Press Flag Hmdx  Hmdx Flag  Wind Chill  Wind Chill Flag Weather  
0             NaN  NaN        NaN         NaN              NaN     NaN  
1             NaN  NaN        NaN         NaN              NaN   Clear  

[2 rows x 25 columns]
</pre>
</div>


<div>
<p><strong>Exercise:</strong> Plot the daily maximum temperature for both August and July</p>
</div>


<div>
<h2 id="key-points">Key Points</h2>
<ul>
<li>Use the <code>pandas.read_csv()</code> to read data from text files into NumPy arrays</li>
<li>Use <code>!</code> to prefix shell commands to execute them from a notebook cell</li>
<li>Use Boolean slices to explore and analyze data</li>
<li>Use requests to download a file</li>
</ul>
</div>


<div class="in">
<pre></pre>
</div>
