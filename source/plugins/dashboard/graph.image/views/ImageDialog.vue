<template>
	<v-card class="graphDialog">
		<v-card-title>{{$t('DASHBOARD_ADDIMAGE')}}</v-card-title>

		<v-card-text class="graphDialog">
			<div layout-padding class="signal-details row">
				<v-text-field autofocus color ="orange" :label="$t('DASHBOARD_SIGNAL_NAME')" required v-model="newdata.id" class="col-md-6">{{$t('DASHBOARD_SIGNAL_NAME')}}</v-text-field>
				<v-text-field :label="$t('NAME')" v-model="newdata.title" class="col-md-6"></v-text-field>
			</div>
			<v-text-field color ="orange" :label="$t('DASHBOARD_SIGNAL_DESCRIPTION')" required v-model="newdata.description" class="col-md-12">{{$t('DASHBOARD_SIGNAL_DESCRIPTION')}}</v-text-field>
			<div class="sig-properties row">
				
				<span class="col-md-12">Links (one image link per row)
					if signal = 0, image from row 1
					if signal = 1, image from row 2
					if signal = 2, image from row 3
				</span>
				<div class="col-md-12">
					<v-textarea outlined required v-model="newdata.imageLinks"></v-textarea>
				</div>
			</div>
		</v-card-text>
		<v-card-actions>
			<v-spacer></v-spacer>
			<v-btn text @click="close">{{$t('CLOSE')}}</v-btn>
			<v-btn class="newapp" text @click="createChart">{{$t('DASHBOARD_ADD_SIGNAL')}}</v-btn>
		</v-card-actions>
		
    </v-card>
</template>

<script>
import _ from 'lodash';

export default {
	name:'ImageDialog',
	components: {
	},
	props:['signal', 'signals', 'data'],
	data() {
		return {
			newdata: _.assign ({
				id:'',
				description:'',
				title: '',
				imageLinks:''
			}, this.data)
		};
	},
	methods: {
		esc() {
			this.close();
		},
		enter() {
			this.createChart();
		}, 
		close ()
		{
			this.$root.$emit('submit');
		},
		createChart()
		{
			let title = this.newdata.id.replace(/ /g,'');
			if(title.length > 0)
				this.$root.$emit ('submit', this.newdata);
			else
				this.studio.workspace.showNotification('DASHBOARD_NO_TITLE');
		}
	}
};
</script>

