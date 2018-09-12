<template lang='pug'>
.layout
	.input-item(
		v-for='item in layout'
		:key='item'
	)
		component(
			:is='formInputs[ fields[item].component ]'
			:options='fields[item].options'
			:fields='fields[item]'
			:errors='errors[item] || {}'

			v-model='childrenValues[item]'
		)
</template>

<script>

const iterate = ( obj, callback ) => {
	if ( Array.isArray( obj ) ) {
		obj.forEach( ( item, i ) => callback( item, i ) );
		return;
	}

	const keys = Object.keys( obj );
	keys.forEach( ( key ) => {
		const item = obj[key];

		callback( item, key );
	} );
};

const clone = ( obj ) => {
	const newObj = Array.isArray( obj ) ? [] : {};

	iterate( obj, ( value, key ) => {
		newObj[key] = typeof value === 'object' ? clone( value ) : value;
	} );

	return newObj;
};

export default {
	name : 'input-layout',

	props : {
		layout : {
			type : [Array, Object]
		},
		fields : {
			type : Object,
		},
		formInputs : {
			type : Object,
		},
		value : {
			type : Object,
		},
		errors : {
			type : Object,
		}
	},

	data : () => ( {
		childrenValues : {},
	} ),

	created() {
		this.childrenValues = clone( this.value );
	},

	watch : {
		childrenValues : {
			deep : true,
			handler( value ) {
				this.$emit( 'input', value );
			}
		}
	},
};
</script>

<style lang='scss'>

.layout {

	.input-item {

		+ .input-item {
			margin-top: 15px;
		}
	}
}
</style>

