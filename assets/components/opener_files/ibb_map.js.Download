/*!
 * BBnaut v1.8.9
 * 2017-10-01
 * Internet Billboard a.s.
 * miza
 */
!function(){function a(){return"http:"===document.location.protocol?"http://":"https://"}function b(a){var b;if("object"==typeof a)b=a;else try{b=JSON.parse(a)}catch(c){return void console.log("Cannot parse ADEX response")}return b&&Array.isArray(b["segment-ids"])&&b["segment-ids"].length>0?b["segment-ids"].toString().replace(/,/g,"-"):void 0}function c(c){var d=b(c);if(d){var f=a()+"bbnaut.ibillboard.com/tag/SdgRtAdex/value/"+d;(new Image).src=f,e()}}function d(){return-1===document.cookie.indexOf(h)}function e(){document.cookie="adex_synced=1; max-age=86400; Path=/"}function f(a){var b=document.createElement("script");b.type="text/javascript",b.async=!0,b.src=a;var c=document.getElementsByTagName("script")[0];c.parentNode.insertBefore(b,c)}function g(){var b=a()+"api.theadex.com/v0.9/pub/segments?access_token=y5fWjpPcqPTEF7fuHtSSUIh1UnD1w2hVEt2Y2PjI&callback=window.ibb_lib.ibb_store";f(b)}const h="adex_synced";window.ibb_lib={},window.ibb_lib.ibb_store=c,d()&&g()}();