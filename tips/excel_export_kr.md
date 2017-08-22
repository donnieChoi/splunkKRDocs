### excel export시 한글 깨짐 현상 해결
<hr />

$SPLUNK_HOME/lib/python2.7/site-packages/splunk/rest/__init__.py 파일 수정

line 668 where it says -- 6.6.0 tested
```
  def readall(self, blocksize=32768):
      """
      Returns a generator reading blocks of data from the response
      until all data has been read
      """
      response = self.response
      while 1:
          data = response.read(blocksize)
          if not data:
             break
         yield data
```
를 하기와 같이 변경
```
  def readall(self, blocksize=32768):
      """
      Returns a generator reading blocks of data from the response
      until all data has been read
      """
      response = self.response
      import codecs
      counter = 0;
      while 1:
         data = response.read(blocksize)
         if not data:
             break

         if counter == 0:
             data = "".join((codecs.BOM_UTF8, data))
             counter += 1

         yield data
```         
and your exports come with BOM.


Answers link
https://answers.splunk.com/answers/128517/how-to-export-csv-with-bom.html
