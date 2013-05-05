CDirectoryCacheDependency-Yii
=============================

#PRINSIP DASAR CARA KERJA CDirectoryCacheDependency

//depedency berdasar file2 yang ada dlm folder ini...
$dependency = new CDirectoryCacheDependency(Yii::app()->basePath.'/../shareimages/photo/');

//cek cache "photolist" udah ada apa belom. jika belom #a jika sudah #b
if (!Yii::app()->cache->get('photolist'.Yii::app()->user->id)) {

//#a. simpan seluruh hasil recursive tampilan photo ke variable $photoList
$photoList=$this->renderPartial("_photoRender",array('contents'=>$contents,'dir'=>$dir,'counter'=>$counter),true);

//simpan variable $photoList ke cache "photolist"
Yii::app()->cache->set('photolist'.Yii::app()->user->id,$photoList,86400,$dependency);
} else

//#b. jika cache "photolist" sudah ada ambil langsung dari cache
$photoList=Yii::app()->cache->get('photolist'.Yii::app()->user->id);

//tampilkan isinya...
echo $photoList;
