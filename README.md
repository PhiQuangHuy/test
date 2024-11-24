- Test and unit test, some test cáse fail because no API from AP
- Backend: Total receivers when update, env vars, code orders -
- Frontend: Reset button in list (datepickr, search bar), excel function, duplicate code -> need reviews
- Test after deployed

document.addEventListener("DOMContentLoaded", () => {
  // Calculate default values
  const now = new Date();
  const oneMonthEarlier = new Date();
  oneMonthEarlier.setMonth(now.getMonth() - 1);

  // Format date to YYYY-MM-DD
  const formatDate = (date) =>
    date.toISOString().split("T")[0]; // Returns the date in YYYY-MM-DD

  const defaultStartDate = formatDate(oneMonthEarlier);
  const defaultEndDate = formatDate(now);

  // Initialize Flatpickr instances
  const startDatePicker = flatpickr("#startDate", {
    defaultDate: defaultStartDate,
    dateFormat: "Y-m-d",
  });

  const endDatePicker = flatpickr("#endDate", {
    defaultDate: defaultEndDate,
    dateFormat: "Y-m-d",
  });

  // Reset button functionality
  document.getElementById("resetButton").addEventListener("click", () => {
    startDatePicker.setDate(defaultStartDate); // Reset start date
    endDatePicker.setDate(defaultEndDate);   // Reset end date
  });
});

