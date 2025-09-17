(function(){

    if (window.location.href.indexOf('/products') === -1) return;

    $('head').append(`
        <style>
            #Popup {
                position: fixed;
                bottom: 80px;
                padding: 10px;
                z-index: 999;
                background-color: #ffffff;
                border-radius: 5px;
                right: 10px;
                box-shadow: 3px 3px 8px 0px #aaaaaa;
                max-width: 450px;
            }

            #Popup__title {
                display: flex;
                gap: 10px;
                margin-bottom: 0.750rem;
            }

            #Popup__title .image {
                flex: 1;
            }

            .h1--popup {
                font-size: 1.4rem;
                margin-bottom: 0;
                flex: 2;
            }

            #Popup .product-single__price {
                font-size: 1rem;
            }

            #Popup .product-form__item label {
                margin-bottom: 7px;
            }

            #Popup form {
                justify-content: end;
            }
        </style>`);

    $('body').append(`
        <div id='Popup'>
            <div id='Popup__title'>
                <div class='image'>
                    <img src='${$('#ProductPhoto img').attr('src')}' />
                </div>
                <div class='h1 h1--popup'>
                    ${ $('.product-single__title').text() }
                </div>
            </div>
        </div>`);

    $('.product-single__meta-list').clone().appendTo('#Popup .h1--popup');

    const $clonedProductTemplate = $('#AddToCartForm-product-template').clone(true, true);
    
    $clonedProductTemplate.find('.shopify-payment-button').remove();

    $clonedProductTemplate
        .insertAfter('#Popup #Popup__title')
        .find('[id]')
        .each((i, el) => {
            $(el).attr('id', `Popup-${ el.id }`);
        });

    const $AddToCartButton = $('#AddToCart-product-template');

    const isPopupElement = (id) => id.indexOf('Popup-') !== -1;

    const bindChangeBehavior = ({ currentTarget }) => {
        const id = currentTarget.id;
        const bindedId = isPopupElement(id) ? `${ id.replace('Popup-', '') }` : `Popup-${ id }`;
        const sourceVal = $(`#${ id }`).val();
        const targetVal = $(`#${ bindedId }`).val();

        if (sourceVal !== targetVal) {
            $(`#${ bindedId }`).val($(`#${ id }`).val()).trigger('change');
        }

        $('#Popup-AddToCart-product-template')
            .prop('disabled', $AddToCartButton.prop('disabled'))
            .attr('class', $AddToCartButton.attr('class'))
            .find('span')
            .text($AddToCartButton.text());
    }

    $('.product-form__item').find('select, input').on('change input', bindChangeBehavior);

    $('.js-qty__adjust').on('click', ({ currentTarget }) => {
        $(currentTarget).parent().find('input').trigger('change');
    })
})();
