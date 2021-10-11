@@ -0,0 +1,20 @@
import http.client
import re

url = 'click1000.training.hackerdom.ru'

headers = {'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/39.0.2171.95 Safari/537.36'}

link_regex = r'<a href=([^ ]*) '

connection = http.client.HTTPSConnection(url)
path = '/start'
while True:
	connection.request('GET', path, headers=headers)
	response = connection.getresponse().read().decode("utf=8")
	match = re.search(link_regex, response)
	if match is not None:
		path = "/" + match.group(1)
	else:
		print(response)
		break
