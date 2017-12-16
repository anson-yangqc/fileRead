## fileRead
## h5 读取本地文件

```javascript
<input type="file" name="" id="csvfile" accept=".csv"/>
```

```javascript
function read2Upload(_this){
		var filePath=$(_this).val();
	        var fileName=getFilename(filePath);
		var fileInput = $(_this)[0];
		var file = fileInput.files[0];
		fileName = fileName || getFilename(fileInput.value);
    	    	if(fileName.indexOf("csv")!=-1){
			if( typeof(FileReader) !== 'undefined' ){    //H5
	     	        	var reader = new FileReader();
	     	        	reader.readAsText(file);            //以文本格式读取
	     	        	if(file.size > 5*1024*1024){
			    	      alert("请上传5M以内的.csv文件");
			    	      return false;
	    	    	 }else{
				reader.onload = function(evt){
				// csvData 是将evt的结果转成与后端协商好的数据格式（一般是数组）
		     	        var data = {"csvData":csvData,"fileName":fileName.substring(0,fileName.indexOf(".csv")),"fileDetails":JSON.stringify({"line":csvData.length,"size":(file.size/1024).toFixed(2)})};
		     	         save(data);//调用后端的保存接口 
	    	    	 	}
		     	 }
			 }else{
				 alert("文件格式不正确,请上传.csv文件");
				 //文件格式不正确
			 }
		}
```
