## sample
```html
<!-- edit-popover -->
<div class="edit-popover">
	<div class="edit-popover-overlay"></div>
	<div class="edit-popover-content"></div>
</div>
```
```css
/* edit-popover */
.edit-popover {
    display: none;
    z-index: 9999;
}

.is_visible {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: block;
    /*justify-content: center;*/
    /*align-items: center;*/
}

.edit-popover-overlay {
    width: 100%;
    height: 100%;
    position: absolute;
}

.edit-popover-content {
    position: absolute;
    background: white;
    margin: 0;
    padding: 7px;
    min-width: 350px;
    max-width: 350px;
    border: 1px solid #cccccc;
    box-shadow: 2px 2px 2px rgba(0, 0, 0, 0.1);
}
/* edit-popover */
```
```js
// 전자지갑 라벨 목록 조회 후 세팅
function getLabels() {
	$.get("/api/wallet/labels", function(rs, status) {
		
		if (status === "success" && rs.status === 200) {
			
			const tags = [];
			
			rs.list.forEach(item => {
				
				const li = document.createElement("li");
				const edit = `<a href="javascript:void(0)"><i class='fa fa-fw fa-edit' style="color: dodgerblue;" data-idx="${ item.labelIdx }" data-title="${ item.title }" onclick="editLabel(e)"></i></a>`;
				const remove = `<a href="javascript:void(0)"><i class='fa fa-trash-o' style="color: orangered" data-idx="${ item.labelIdx }" data-title="${ item.title }" onclick="removeLabel(e)"></i></a>`;
				
				li.style.cssText = "min-width: 260px; display: flex; justify-content: space-between;";
				li.innerHTML = `<a href="#" class="width70Per paddingT7" data-idx=${ item.labelIdx }>${ item.title }</a><span class="paddingLR20"> ${ edit } &nbsp; ${ remove } </span>`;
				
				tags.push(li);
			});
			
			tags.push(`<li role="separator" class="divider"></li>`);
			tags.push(`<li><a href="#" class="customNewLabel">새로 만들기</a></li>`);
			
			$("#walletLabelList").empty().html(tags);
			
			// [수정],[삭제] 아이콘 클릭시 dropdown-menu 창이 닫히는 것을 막는다
			document.querySelectorAll("#walletLabelList span").forEach(item => {
				item.addEventListener("click", e => e.stopPropagation());
			});
		}
	});
}

// 라벨 수정
function editLabel(e) {
	
	// set popover controller & content
	const popover = document.querySelector(".edit-popover");
	const overlay = document.querySelector(".edit-popover-overlay");
	const popoverContent = document.querySelector(".edit-popover-content");
	
	popoverContent.innerHTML = `<div class="form-group zeroMargin">
		<div class="input-group">
			<input type="text" class="form-control" name="labelTitle" placeholder="라벨명" autocomplete="off">
			<span class="input-group-btn">
				<button type="button" class="btn btn-primary" name="editBtn">수정</button>
				<button type="button" class="btn btn-default" name="cancelBtn">취소</button>
			</span>
		</div>
	</div>`;
	
	const editBtn = document.querySelector("[name=editBtn]");
	const cancelBtn = document.querySelector("[name=cancelBtn]");
	
	// show popover
	popover.classList.add("is_visible");
	
	// force stop propagation
	popover.addEventListener("click", e => e.stopPropagation());
	
	// set [x],[y] position
	popoverContent.style.top = `${ e.clientY - 25 }px`;
	popoverContent.style.left = `${ e.clientX - 25 }px`;
	
	// close popover
	function closePopover() {
		popover.classList.remove("is_visible");
		popoverContent.innerHTML = "";
	}
	
	overlay.addEventListener("click", closePopover);
	cancelBtn.addEventListener("click", closePopover);
	
	// check editable
	if (!e.target.dataset.idx || !e.target.dataset.title) {
		alert("수정할 라벨 정보가 존재하지 않습니다\n다시 확인해 주세요.");
		return false;
	}
	
	// set value
	document.querySelector("[name=labelTitle]").dataset.idx = e.target.dataset.idx;
	document.querySelector("[name=labelTitle]").value = e.target.dataset.title;
	document.querySelector("[name=labelTitle]").focus();
	
	// update value
	editBtn.addEventListener("click", e => {
		
		const param = {
			labelIdx : document.querySelector("[name=labelTitle]").dataset.idx,
			title : document.querySelector("[name=labelTitle]").value
		};
		
		$.ajax({
			url : "/api/wallet/label",
			type : "PUT",
			data : param,
			async : false, // 더블클릭 방지
			dataType : "json"
		}).done(() => {
			getLabels();
		}).fail(error => {
			alert(`error : ${ error }`);
		}).always(() => {
			closePopover();
		});
	});
}

// 라벨 삭제
function removeLabel(e) {
	
	if (!e.target.dataset.idx || !e.target.dataset.title) {
		alert("삭제할 라벨 정보가 존재하지 않습니다\n다시 확인해 주세요.");
		return false;
	}
	
	if (!confirm(`[ ${ e.target.dataset.title } ] 라벨을 삭제하시겠습니까?`)) {
		e.stopPropagation();
		return false;
	}
	
	$.ajax({
		url : "/api/wallet/label",
		type : "DELETE",
		data : { labelIdx : e.target.dataset.idx },
		async : false, // 더블클릭 방지
		dataType : "json"
	}).done(() => {
		getLabels();
	}).fail(error => {
		alert(`error : ${ error }`);
	});
}
```
