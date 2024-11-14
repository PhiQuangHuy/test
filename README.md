const today = new Date();
const oneMonthAgo = new Date(today.setMonth(today.getMonth() - 1));

const startDateInput = $('#startDate').flatpickr({
  dateFormat: 'Y-m-d',
  defaultDate: oneMonthAgo,
  onChange: function(selectedDates, dateStr, instance) {
    endDateInput.set('minDate', dateStr);
    endDateInput.setDate(selectedDates[0]);
  }
});

const endDateInput = $('#endDate').flatpickr({
  dateFormat: 'Y-m-d',
  defaultDate: today,
  minDate: oneMonthAgo
});
