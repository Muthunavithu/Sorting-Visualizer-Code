async function insertion(){
    document.getElementById('outputParent').classList.add("d-none");
    
    const ele = document.querySelectorAll(".bar");
    // color
    ele[0].style.background = 'green';
    for(let i = 1; i < ele.length; i++){
        
        let j = i - 1;
        let key = ele[i].style.height;
        // color
        ele[i].style.background = 'blue';

        await waitforme(delay);

        while(j >= 0 && (parseInt(ele[j].style.height) > parseInt(key))){
            
            // color
            ele[j].style.background = 'blue';
            ele[j + 1].style.height = ele[j].style.height;
            ele[j + 1].setAttribute('org', parseInt(ele[j].style.height)/2);
    

            j--;

            await waitforme(delay);

            // color
            for(let k = i; k >= 0; k--){
                ele[k].style.background = 'green';
            }
        }
        ele[j + 1].style.height = key;
        ele[j + 1].setAttribute('org', parseInt(key)/2);
        
        // color
        ele[i].style.background = 'green';
    }
}

const inSortbtn = document.querySelector(".insertionSort");
inSortbtn.addEventListener('click', async function(){
    disableSortingBtn();
    disableSizeSlider();
    disableNewArrayBtn();
    await insertion();
    let HTMLelements =
            document.getElementsByClassName("bar");
            let sortedarray = [];
        for (elem of HTMLelements) {
            // Print the current element
            
            sortedarray.push(elem.getAttribute('org'));
        }
    document.getElementById('outputChildDivId').innerHTML = "["+sortedarray+"]";
    
    enableSortingBtn();
    enableSizeSlider();
    enableNewArrayBtn();
    document.getElementById('outputParent').classList.remove("d-none");
});