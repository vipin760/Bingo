var url = window.location.href;
//var hash = window.location.hash.substring(1);
var altTag;
var cvideo = $('#player').attr('data-id');
// 2. This code loads the IFrame Player API code asynchronously.
      var tag = document.createElement('script');

      tag.src = "//www.youtube.com/iframe_api";
      var firstScriptTag = document.getElementsByTagName('script')[0];
      firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);

      // 3. This function creates an <iframe> (and YouTube player)
      //    after the API code downloads.
      var player;
      function onYouTubeIframeAPIReady() {
        player = new YT.Player('player', {
         playerVars: {
            autoplay: 0,
            rel : 0,
        },
          videoId: $('#player').attr('data-id'),
          
          events: {
            'onReady': onPlayerReady,
            'onStateChange': onPlayerStateChange
          }
        });
      }

      // 4. The API will call this function when the video player is ready.
      function onPlayerReady(event) {
        //event.target.playVideo();
      }

      // 5. The API calls this function when the player's state changes.
      //    The function indicates that when playing a video (state=1),
      //    the player should play for six seconds and then stop.
      var done = false;
      function onPlayerStateChange(event) {
        if (event.data == YT.PlayerState.PLAYING && !done) {
         // setTimeout(stopVideo, 6000);
         // done = true;
        }
      }
      function stopVideo() {
        player.stopVideo();
      }

    function showRequest(formData, jqForm, options) { 
    

        var queryString = $.param(formData); 
	
		var topTextBox = $("#topTextBox").val();
        var bottomTextBox = $("#bottomTextBox").val();
		var img = $("#image").val();
        var file = $('#uimg').val();
        if(topTextBox == "" )
		{
			bootbox.alert("You cannot have an empty top text field");
			return false;
		}
		else if(bottomTextBox.trim() == "")
		{
			bootbox.alert("You cannot have an empty bottom text field");
			return false;
		}
        else if(img.trim() == "" && file == "")
		{
			bootbox.alert("Please select or upload an image to continue");
			return false;
		}
        
    
    
		$('.submit-btn').prop('disabled', true);
    
        $(".overLay").show();
        $(".loader").show();
     
		 return true;
}
		

function showResponse(responseText, statusText, xhr, $form)  { 
    
   console.log(responseText);
    var data = JSON.parse(responseText);
	if (data.status.trim() == 'success')
	{ 
        window.location.href = data.img;        
	}
	else if (responseText.trim() == 'You are already registered')
	{ 
         bootbox.alert("Please select an image to continue");
	}
    else if (responseText.trim() == 'entries closed')
    {
        
    }
    else if(responseText.trim() == "Not")
    {
        
    }
	
}

function Upload(size) {
    //Get reference of FileUpload.
    var fileUpload = document.getElementById("uimg");
 
    //Check whether the file is valid Image.
 
        //Check whether HTML5 is supported.
        if (typeof (fileUpload.files) != "undefined") {
            //Initiate the FileReader object.
            var reader = new FileReader();
            //Read the contents of Image File.
            reader.readAsDataURL(fileUpload.files[0]);
            reader.onload = function (e) {
                //Initiate the JavaScript Image object.
                var image = new Image();
 
                //Set the Base64 string return from FileReader as source.
                image.src = e.target.result;
                       
                //Validate the File Height and Width.
                image.onload = function () {
                    var height = this.height;
                    var width = this.width;
                    if (height > 600 || width > 600) {
                        bootbox.alert("Height and Width must not exceed 600px.");
                        $("#uimg").val('');
                        return false;
                    }
                    else if(size > 5242880)
                    {
                        bootbox.alert("File size must not exceed 5mb.");
                        $("#uimg").val('');
                        return false;     
                    }
                    else
                    {
                        $('#mg-image').attr('src', e.target.result)
                    }
                    
                    
                    return true;
                };
 
            }
        } else {
            alert("This browser does not support HTML5.");
            return false;
        }
    
}

$uploadCrop = $('#upload-demo').croppie({
                    viewport: {
                        width: 600,
                        height: 600,
                        type: 'square'
                    },
                    enableExif: true,
                    enableZoom: false
                });

function readImage1(e) {
    var t = new FileReader,
    n = new Image;
    t.readAsDataURL(e), t.onload = function(t) 
    {
        n.src = t.target.result, n.onload = function() 
        {
            this.width, this.height, e.type, e.name, ~~(e.size / 1024) + "KB";
            var msize = 5120;
            var size = e.size / 1024 ;
            console.log(this.width+' image '+this.height);
            if(size > msize)
            {
                bootbox.alert("File size limit is 5 mb", function() {});
            }
            else 
            { 
                $('#ext').val(e.type);
                $('.upload-demo').addClass('ready'); 
                $('.cropWrapper').show(); 
                $('#upload-demo').croppie('bind', { url: t.target.result }).then(function(){ 
                    console.log('jQuery bind complete'); 
                }); 
            } 
        }, n.onerror=function() { alert("Invalid file type: " + e.type) }
    }
}


$(document).ready(function() {

    $('.closeCrop').click(function(){
        $('.cropWrapper').hide();
    });
    
    	
    $('#topTextBox').keyup(function() {
        $('#targetTop').html($(this).val());
    });
            
    $('#bottomTextBox').keyup(function() {
        $('#targetBottom').html($(this).val());
    });
    
   $('#uimg').on('change', function () { readImage1(document.getElementById("uimg").files[0]); });
    $('.upload-result').on('click', function (ev) {
            $('.ag-loader1').show();
           
            $uploadCrop.croppie('result', {
                type: 'canvas',
                size: 'viewport'
            }).then(function (resp) {
                console.log(resp);
                var t = $('#ext').val();
                
                $.post( "http://bingosnacks.com/wp-content/themes/bingo/ajaxpro.php", { image: resp, type: t}).done(function( data ) {
                    var data = JSON.parse(data);
                    console.log(data);
                    if(data.status == 'success')
                    {
                        $('.ag-loader1').hide();
                        $('#mg-image').attr('src', "http://bingosnacks.com/wp-content/themes/bingo/"+data.path);
                        $('#image').val(data.path);
                        $(".cropWrapper").hide();
                       
                    }
                });
               
               
               
            });
        });
    
    
    $('#topTextBox').filter_input({regex:'[a-zA-Z ]'});
    $('#bottomTextBox').filter_input({regex:'[a-zA-Z ]'});
    
    $('.template').click(function(){
       var img = $(this).attr('src');
        $('#mg-image').attr('src', img);
        var v = img.split("makeme-img");
        $('#image').val('makeme-img'+v[1]);
        var h = $('#header').height();
        $('html, body').animate({
        scrollTop: $("#makeMeme").offset().top - h
    }, 2000);
    });
    
    var options = { 
        beforeSubmit:  showRequest, 
        success:       showResponse
    };
    
    $('#dform').ajaxForm(options); 
    
    
    
    var pgurl = window.location.href;
    
    var showcase = $("#showcase");

    showcase.Cloud9Carousel({
        buttonLeft: $(".nav > .left"),
        buttonRight: $(".nav > .right"),
        autoPlay: false,
        bringToFront: true,
		handle: 'carousel',
		frontItemClass: 'carActive',
        //onRendered: showcaseUpdated,
        onLoaded: function() {
            showcase.css('visibility', 'visible')
            showcase.css('display', 'none')
            showcase.fadeIn(1500)
        }
    });
  
	$('.dmhashmenu').click(function(){
			
console.log($(this).attr("href"));
		/*window.location.href = $(this).attr("href");
		setInterval(function(){
			location.reload(true);
		}, 300);*/
		
	});
	
	
    
    if(pgurl == '' || pgurl == 'undefined' || pgurl == null)
    {
        $('#homeMenu').addClass('menu-active');
    }
    else if(pgurl.indexOf("bingo-yumitos") >=0 || pgurl.indexOf("mad-angles") >=0 || pgurl.indexOf("bingo-tangles") >=0 || pgurl.indexOf("bingo-tedhe-medhe") >=0 || pgurl.indexOf("bingo-no-rulz") >=0 )
    {
        $(".nav-menu li").each(function(){
            $(this).removeClass('menu-active');
        });
        $('#snackMenu').addClass('menu-active');       
    }
    else if(pgurl.indexOf("blog") >=0)
    {
        $(".nav-menu li").each(function(){
            $(this).removeClass('menu-active');
        });
        $('#blogMenu').addClass('menu-active');
    }
    else
    {
        $(this).removeClass('menu-active');
        $(".nav-menu li").each(function(){
         
         var hlink =  $(this).find('a').attr("href")+'/';
          if(hlink == pgurl)
            {
                $(this).addClass("menu-active");
                console.log('testing 123');
            }
     });
    }
    
     
    
    /*Comedy Adda*/
    
    $(".play-video img").click(function(){
           var dataId = $(this).attr("data-video-id");
          //alert(dataId);
          player.cueVideoById(dataId);
          player.playVideo();
          jQuery('html, body').animate({
			scrollTop: jQuery('.videowrap').offset().top -150
		}, 800);
           
        });
    
    
    $('.vthumbnail').click(function(){
        var dataId = $(this).attr("data-video-id");
          //alert(dataId);
          player.cueVideoById(dataId);
          player.playVideo();
          /*jQuery('html, body').animate({
			scrollTop: jQuery('.videowrap').offset().top -150
		}, 800);*/
    });
        
        $(".play-video").click(function () {
          $('.play-video').removeClass("activeVideo");
           $(this).addClass("activeVideo");
         });
    
    
    $(".rig-cell").click(function () {
          $('.rig-cell').removeClass("active-rig-cell");
           $(this).addClass("active-rig-cell");
         });
    
    
	/*Comedy Adda*/
    
    /*active-menu*/
    /*$(".nav-menu li").click(function () {
          $('.nav-menu li').removeClass("menu-active");
           $(this).addClass("menu-active");
         });*/
   /*active-menu*/
    
    
    

    
    
    if(hash != "")
	{
        $('.productDescription').hide();
        $('.'+hash).show();
        
        $('.cloud9-item').each(function(){
            var d = $(this).attr('data-id');
            var index = '';
            if(d == hash)
            {
                index = $(this).attr('data-slide');
                //showcase.goTo(index);
            }
            
        });
		
	}
    
	
	$("#showcase img").click(function () {
		altTag = $(this).attr('alt');
        $('.productDescription').hide();
        console.log(altTag);
        $('.'+altTag).show();
		window.location.hash = altTag;
	});
	
	//$('#footer').load("common/footer.html");
	if (screen.width > 1025) {
         var divHeight = $('.leftCont').outerHeight();
        $('.rightCont').css('height', divHeight + 'px');

        var divHeightOne = $('.leftmemeCont').outerHeight();
        $('.rightmemeCont').css('height', divHeightOne + 'px');
		
//		var divHeightTwo = $('.videowrap').outerHeight();
//        $('.videoCont').css('height', divHeightTwo + 'px');
		
		
    }
    $('.slider-for').slick({
        slidesToShow: 1,
        slidesToScroll: 1,
        arrows: false,
        fade: true,

        asNavFor: '.slider-nav'
    });
    $('.slider-nav').slick({
        slidesToShow: 4,
        slidesToScroll: 1,
        asNavFor: '.slider-for',
        dots: false,
        infinite: true,
        centerMode: false,
        vertical: true,
        arrows: false,
        focusOnSelect: true,
        responsive: [{
            breakpoint: 1024,
            settings: {
                slidesToShow: 2,
                slidesToScroll: 1,
                infinite: true,
                vertical: false,
                arrows: false,
                dots: false
            }
        }, {
            breakpoint: 600,
            settings: {
                slidesToShow: 1,
                slidesToScroll: 1,
                vertical: false
            }
        }, {
            breakpoint: 480,
            settings: {
                slidesToShow: 1,
                slidesToScroll: 1,
                adaptiveHeight: true,
                vertical: false,
                autoplay: false,
                autoplaySpeed: 6000,
                centerMode: true,
                centerPadding: '40px',
                arrows: true
            }
        }]
    });
    
    
    /*TVC*/
    
    $('#grid').mediaBoxes({
			filterContainer: '#filter',
			search: '#search',
			sortContainer: '#sort1',
			getSortData: {
				title: '.media-box-title',
				year: '.media-box-date parseInt',
			},
			boxesToLoadStart: 9,
			boxesToLoad: 10,
			horizontalSpaceBetweenBoxes: 20,
			verticalSpaceBetweenBoxes: 20,
		});

		$('#grid2').mediaBoxes({
			filterContainer: '#filter2',
			sortContainer: '#sort',
			getSortData: {
				title: '.media-box-title',
				year: '.media-box-year parseInt',
				author: '.media-box-author'
			},
			horizontalSpaceBetweenBoxes: 20,
			verticalSpaceBetweenBoxes: 20,
		});

		$('#grid3').mediaBoxes({
			filterContainer: '#filter3',
			search: '#search2',
			sortContainer: '#sort2',
			getSortData: {
				title: '.media-box-title',
				year: '.media-box-date parseInt',
			},
			boxesToLoadStart: 9,
			boxesToLoad: 10,
			horizontalSpaceBetweenBoxes: 20,
			verticalSpaceBetweenBoxes: 20,
		});
    
    /*TVC*/
    
    jQuery(function($) {

  $(".option-heading").click(function() {
    $(this).next(".option-content").stop().slideToggle(500);
    $(this).find(".arrow-up, .arrow-down").toggle();
  });

});
    
	
});
(function($) {

    //Function to animate slider captions 
    function doAnimations(elems) {
        //Cache the animationend event in a variable
        var animEndEv = 'webkitAnimationEnd animationend';

        elems.each(function() {
            var $this = $(this),
                $animationType = $this.data('animation');
            $this.addClass($animationType).one(animEndEv, function() {
                $this.removeClass($animationType);
            });
        });
    }

    //Variables on page load 
    var $myCarousel = $('#carousel-example-generic'),
        $firstAnimatingElems = $myCarousel.find('.item:first').find("[data-animation ^= 'animated']");

    //Initialize carousel 
    $myCarousel.carousel();

    //Animate captions in first slide on page load 
    doAnimations($firstAnimatingElems);

    //Pause carousel  
    $myCarousel.carousel('pause');


    //Other slides to be animated on carousel slide event 
    $myCarousel.on('slide.bs.carousel', function(e) {
        var $animatingElems = $(e.relatedTarget).find("[data-animation ^= 'animated']");
        doAnimations($animatingElems);
    });

})(jQuery);
$(function() {
	
    

    /* function showcaseUpdated(showcase) {
        var title = $('#item-title').html(
            $(showcase.nearestItem()).attr('alt')
        )

        var c = Math.cos((showcase.floatIndex() % 1) * 2 * Math.PI)
        title.css('opacity', 0.5 + (0.5 * c))
    } */

    // Simulate physical button click effect
    /* $('.nav > button').click(function(e) {
        var b = $(e.target).addClass('down')
        setTimeout(function() {
            b.removeClass('down')
        }, 80)
    }) */

    /* $(document).keydown(function(e) {
        //
        // More codes: http://www.javascripter.net/faq/keycodes.htm
        //
        switch (e.keyCode) {
            case 37:
                $('.nav > .left').click()
                break

            case 39:
                $('.nav > .right').click()
        }
    }) */
});
/*$(window).load(function () {
	if (screen.width > 1025) {
		var divHeight = $('.leftCont').outerHeight();
        $('.rightCont').css('height', divHeight + 'px');

        var divHeightOne = $('.leftmemeCont').outerHeight();
        $('.rightmemeCont').css('height', divHeightOne + 'px');
		
//		var divHeightTwo = $('.videowrap').outerHeight();
//        $('.videoCont').css('height', divHeightTwo + 'px');
	
    }
	if(hash != "")
	{
		$('.rightContNew').load('common/'+hash+'.html');
		
	}
});*/
$(window).load(function () {
	var hash1 = hash;	
	//if(window.location.href.indexOf('#'+hash1) > -1) {
		$(".cloud9-item").each(function() {
			var getDataId = $(this).attr('data-slide');
			var did = $(this).attr('data-id');
			if(hash1 == did)
			{
				$("#showcase").data("carousel").goTo( getDataId );
			}
			
		});		
	//}
});
$(function () {
	var blogDivheight = $('.blogDivLeft').height();
		$('.blogDivRight').css('height', blogDivheight+'px');
});



