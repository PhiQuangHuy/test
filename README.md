$('#select-all').on('change', function () {
    const isChecked = $(this).is(':checked');

    $('.checkbox-item').each(function () {
        const value = $(this).val();
        const dataType = $(this).data('type');

        if (isChecked) {
            // Check all checkboxes
            $(this).prop('checked', true);
            if (dataType === 'normal' && !norArray.includes(value)) {
                norArray.push(value);
            } else if (dataType === 'new' && !newArray.includes(value)) {
                newArray.push(value);
            }
        } else {
            // Uncheck all checkboxes
            $(this).prop('checked', false);
            if (dataType === 'normal') {
                norArray = [];
            } else if (dataType === 'new') {
                newArray = [];
            }
        }
    });

    console.log('norArray:', norArray);
    console.log('newArray:', newArray);
});

Please check the following 2 issues:
1, API sendMsgDetails still not remove email mask current update screen not working
2, API to search user not working when token expires
