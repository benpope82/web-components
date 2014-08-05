web-components
==============

Powerful super-minimal web components

````
<!DOCTYPE HTML>
<hello x-custom name='world'></hello>
<br>
<hellobj x-custom id='me' name='world'>A callable JS object</hellobj>

<script>
window.onload = function() {
  var es = document.querySelectorAll('[x-custom]');
  Array.prototype.forEach.call(es, function(e) {
    var p = {};
    [].slice.call(e.attributes).forEach(function(a) {
      p[a.nodeName] = a.value;
    })
    var ret = window[e.localName].call(null, p, e);
    typeof ret === 'object' ? window[e.id] = ret : e.innerHTML = ret;
  })
  ready();
}

function hello(p, e) {
  return 'hello ' + p.name;
}

function hellobj(p, e){
  return {
  	 e: e,
  	 alert: function(){
  	 	alert('hello ' + p.name);
  	 }
  }
}

function ready(){
  me.alert();
}
</script>
````
