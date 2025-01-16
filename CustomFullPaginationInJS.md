### Just you need to add selector of a list wrapper and list-child-item according to your html structure. 
###  'active' class is added to the current active pager. You can style your pagination according to your requirement

```javascript
let listWrapperSelector = '.list-wrapper';
let listChildItemSelector = '.list-wrapper > .list-item';


// Function to generateNewPagination on each pagerBtn click
    function generateNewPagination(currentPagerIndex,totalPagerCount, listChildItemSelector){
         let listItems = document.querySelectorAll(listChildItemSelector);
        let listItemCount = listItems.length;
          let fromIndex = (currentPagerIndex * 10) - 10; 
        let toIndex = Math.min(currentPagerIndex * 10, listItemCount);
        
       
           for(let i = 0; i!= listItemCount;i++){
               listItems[i].classList.add('hide');
            }
            
      for(let i = fromIndex; i!= toIndex;i++){
               listItems[i].classList.remove('hide');
        }
        if(currentPagerIndex==1){
            document.querySelector('.pagerContainer .prev').classList.add('hide');
            document.querySelector('.pagerContainer .first').classList.add('hide');
        }else{
            document.querySelector('.pagerContainer .prev').classList.remove('hide');
             document.querySelector('.pagerContainer .first').classList.remove('hide');
        }
        if(currentPagerIndex==totalPagerCount){
            document.querySelector('.pagerContainer .next').classList.add('hide');
            document.querySelector('.pagerContainer .last').classList.add('hide');
        }else{
            document.querySelector('.pagerContainer .next').classList.remove('hide');
             document.querySelector('.pagerContainer .last').classList.remove('hide');
        }
    }




const list = document.querySelector(listWrapperSelector);

let pagerContainer = document.createElement('div');
pagerContainer.classList.add('pagerContainer');
list.appendChild(pagerContainer);

let listItemCount = list.children.length - 1;
let totalPagerCount = Math.ceil(listItemCount/10); 

if(totalPagerCount>1){
    // Adding firstButton in pagerContainer
    let firstButton = document.createElement('button');
    firstButton.classList.add('first');
    firstButton.innerText = 'First'
    pagerContainer.appendChild(firstButton);
    
    // Adding PrevButton in pagerContainer
    let prevButton = document.createElement('button');
    prevButton.classList.add('prev');
    prevButton.innerText = 'Prev'
    pagerContainer.appendChild(prevButton);
     
    //  Adding all pager btns according to totalPagerCount
    for(let i=1;i<=totalPagerCount;i++){
        let pagerBtn = document.createElement('button');
        pagerBtn.classList.add('pagerBtn')
        pagerBtn.innerText = i;
        pagerContainer.appendChild(pagerBtn);
    }
    
    // Adding nextButton in pagerContainer
    let nextButton = document.createElement('button');
    nextButton.classList.add('next');
    nextButton.innerText = 'Next'
    pagerContainer.appendChild(nextButton);
    
    // Adding lastButton in pagerContainer
    let lastButton = document.createElement('button');
    lastButton.classList.add('last');
    lastButton.innerText = 'Last'
     pagerContainer.appendChild(lastButton);
    
    
    
    // By default, making firstPager active
    let firstPager = document.querySelectorAll('.pagerContainer .pagerBtn')[0];
    firstPager.classList.add('active');
    
    // Defining page change functionality on each pager click
    let allPagers = document.querySelectorAll('.pagerContainer .pagerBtn')
    let currentPagerIndex = 1; //By default currentPagerIndex will be 1 
    
      for(let i=0;i!=totalPagerCount;i++){
        allPagers[i].addEventListener('click',()=>{
            currentPagerIndex = i+1; // Updating currentPagerIndex on each pager Click
            allPagers[i].classList.add('active') //Adding active class to current clicked pager
            
            // Removing active class from all other pager than current clicked pager
            for(let j=0;j!=totalPagerCount;j++){
                if(j==i)
                continue;
                else
                allPagers[j].classList.remove('active')
            }
            //Generated the pagination according to current active pager
            generateNewPagination(currentPagerIndex,totalPagerCount,listChildItemSelector);
        })
        
        
        }
        
        // Defining page change functionality on prevButton click
        prevButton.addEventListener('click',()=>{
            if(currentPagerIndex!=1){
                currentPagerIndex--;
            }
            let activePager = allPagers[currentPagerIndex-1];
            activePager.classList.add('active');
             for(let j=0;j!=totalPagerCount;j++){
                if(j==currentPagerIndex-1)
                continue;
                else
                allPagers[j].classList.remove('active')
            }
            //Generated the pagination according to current active pager
            generateNewPagination(currentPagerIndex,totalPagerCount,listChildItemSelector);
        });
        
        
        // Defining page change functionality on firstButton click
           firstButton.addEventListener('click',()=>{
           currentPagerIndex = 1;
            let activePager = allPagers[0];
            activePager.classList.add('active');
             for(let j=0;j!=totalPagerCount;j++){
                if(j==currentPagerIndex-1)
                continue;
                else
                allPagers[j].classList.remove('active')
            }
            //Generated the pagination according to current active pager
            generateNewPagination(currentPagerIndex,totalPagerCount,listChildItemSelector);
            
        });
        
        // Defining page change functionality on lastButton click
              lastButton.addEventListener('click',()=>{
           currentPagerIndex = totalPagerCount;
            let activePager = allPagers[totalPagerCount-1];
            activePager.classList.add('active');
             for(let j=0;j!=totalPagerCount;j++){
                if(j==currentPagerIndex-1)
                continue;
                else
                allPagers[j].classList.remove('active')
            }
            //Generated the pagination according to current active pager
            generateNewPagination(currentPagerIndex,totalPagerCount,listChildItemSelector);
        });
        
        // Defining page change functionality on nextButton click
           nextButton.addEventListener('click',()=>{
            if(currentPagerIndex!=totalPagerCount){
                currentPagerIndex++;
            }
            let activePager = allPagers[currentPagerIndex-1];
            activePager.classList.add('active');
             for(let j=0;j!=totalPagerCount;j++){
                if(j==currentPagerIndex-1)
                continue;
                else
                allPagers[j].classList.remove('active')
            }
           //Generated the pagination according to current active pager
            generateNewPagination(currentPagerIndex,totalPagerCount,listChildItemSelector);
        });

//Generated the pagination by default 
generateNewPagination(currentPagerIndex,totalPagerCount,listChildItemSelector); 
}      
```

### This example is according to this html structure.
```html
<section class="list-wrapper">
    <div class='list-item'>1</div>
    <div class='list-item'>2</div>
    <div class='list-item'>3</div>
    <div class='list-item'>4</div>
    <div class='list-item'>5</div>
    <div class='list-item'>6</div>
    <div class='list-item'>7</div>
    <div class='list-item'>8</div>
    <div class='list-item'>9</div>
    <div class='list-item'>10</div>
     <div class='list-item'>11</div>
    <div class='list-item'>12</div>
    <div class='list-item'>13</div>
    <div class='list-item'>14</div>
    <div class='list-item'>15</div>
    <div class='list-item'>16</div>
    <div class='list-item'>17</div>
    <div class='list-item'>18</div>
    <div class='list-item'>19</div>
    <div class='list-item'>20</div>
     <div class='list-item'>21</div>
    <div class='list-item'>22</div>
    <div class='list-item'>23</div>
    <div class='list-item'>24</div>
    <div class='list-item'>25</div>
</section>
