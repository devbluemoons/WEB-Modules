## Grobal Variable
[Ref.] https://stackoverflow.com/questions/12393303/storing-a-variable-in-the-javascript-window-object-is-a-proper-way-to-use-that  
  
```js
window.validEvents = {
	"click #btnDelete" : function(e, value, row, index) {
		const data = {
			parcelHolidayIdx : row.parcelHolidayIdx,
			valid : false
		};
		$.ajax({
			url : "/api/parcel/holiday/valid",
			type : "PUT",
			data : data,
			async : false, // 더블클릭 방지
			dataType : "json",
			success : function(rs, status) {
				if (status == "success") {
					row.valid = false;
					$("#table").bootstrapTable("updateRow", {
						index : index,
						row : row
					});
				}
			}
		});
	},
	"click #btnRecover" : function(e, value, row, index) {
		const data = {
			parcelHolidayIdx : row.parcelHolidayIdx,
			valid : true
		};
		$.ajax({
			url : "/api/parcel/holiday/valid",
			type : "PUT",
			data : data,
			async : false, // 더블클릭 방지
			dataType : "json",
			success : function(rs, status) {
				if (status == "success") {
					row.valid = true;
					$("#table").bootstrapTable("updateRow", {
						index : index,
						row : row
					});
				}
			}
		});
	}
};
```
