# numberroduction
This is public user documentation for V2.0 of Orbits Lua Engine. This lists everything you would need to know to start creating scripts. 
`last updated 11/14/21`

### __Menu Features__ 
Features are used to interact with the user interface, creating native-like options in the Orbit UI.
To create a new feature use `menu.add_feature(string name, string type, number parent, function)`, this returns a Feature object. The function argument is called with the feature object as an argument when the feature is pressed.

You can also add player features, these will be shown for each player in the session `menu.add_player_feature(string name, string type, number parent, function)`. Same applies for function except there is also a second argument with the target Player.

### __Feature Types__

|Type|Usage|
|-|-|
|parent|Parent feature, creates a new submenu|
|action|This is a basic feature which only has a click functionality|
|toggle|Toggle Feature|
|value_i, value_f, action_value_i, action_value_f|All of these are the same but exist for compatibility with scripts, and uses the `value` property of the Feature object|

### __Feature Object Types__
```
@ id
@ name
@ hidden
@ on
@ value
@ min
@ max
@ mod
--- Legacy Support ---
@ value_i
@ min_i
@ max_i
@ mod_i
```

### __Menu Functions__
```
Feat             add_feature(string name, string type, number parent, function callback)
Feat             add_player_feature(string name, string type, number parent, function callback, number playerID)
Feat             get_player_feature(number id)
boolean          delete_feature(number id)
boolean          delete_player_feature(number id)
string           get_version()
boolean          is_trusted_mode_enabled()
nill             notify(string text)
```

### __D3D Functions__
```
nill             set_next_window_pos(v2 pos)
nill             begin(string name, booleanopen, number flags)
nill             end()
nill             text_label(string name, string text)
nill             text(string text)
boolean          button(string label)
boolean          selectable(string label, booleanselected)
boolean          slider_number(string label, number v, number min, number max)
boolean          slider_number(string label, number v, number min, number max)
boolean          tree_node(string label)
nill             tree_pop()
nill             separator()


```

### __Handlers__
```
Handler          Initialize(Feat feat, * data)
Handler          OnDxOptionsTick(Feat feat)
Handler          Tick(Feat feat, * data)
```

### __Classes__

 __Color__
|Property|Usage|Min|Max|
|-|-|-|-|
|r|Red value|0|255|
|g|Green value|0|255|
|b|Blue value|0|255|
|a|Alpha value|0|255|

 v2 
```
@property      number       x
@property      number       y

@method v2      __add(v2|v3|number)
@method v2      __sub(v2|v3|number)
@method v2      __mul(v2|v3|number)
@method v2      __div(v2|v3|number)
@method boolean__eq(v2)
@method boolean__lt(v2)
@method boolean__le(v2)
@method string  __tostring()
@method number   magnitude(v2|nill)
```
 v3 
```
@property      number       x
@property      number       y
@property      number       z

@constructor    v3()
@constructor    v3(number)
@constructor    v3(number, number, number)

@method v3      __add(v2|v3|number)
@method v3      __sub(v2|v3|number)
@method v3      __mul(v2|v3|number)
@method v3      __div(v2|v3|number)
@method boolean__eq(v3)
@method boolean__lt(v3)
@method boolean__le(v3)
@method string  __tostring()
@method number   magnitude(v3|nill)
@method nill     transformRotToDir()
@method nill     radToDeg()
@method nill     degToRad()
```

### __Hook Functions__

```
hook            hook.register_script_event_hook(funtion callback)
hook            hook.register_net_event_hook(funtion callback)
boolean         hook.remove_script_event_hook(number id)
boolean         hook.remove_net_event_hook(number id)
```

 __Hooks__

````
nill             script_event_hook(Player sender, number[] args, number args, number params)
nill             script_event_hook(Player sender, Player target, number eventIds)
````

___

### __RAGE__

 __Player Functions__ 
```
Ped              get_player_ped(Player player)
Player           player_id()
nill             set_player_model(Hash hash)
nill             get_player_group(Player player)
boolean          is_player_female(Player player)
boolean          is_player_friend(Player player)
boolean          is_player_playing(Player player)
boolean          is_player_free_aiming(Player player)
Entity           get_entity_player_is_aiming_at(Player player)
nill             set_player_visible_locally(Player player, boolean toggle)
nill             set_player_as_modder(Player player)
string           get_player_name(Player player)
number           get_player_scid(Player player)
boolean          is_player_pressing_horn(Player player)
boolean          is_player_modder(Player player)
boolean          is_player_god(Player player)
number           get_player_wanted_level(Player player)
number           player_count()
boolean          is_player_in_any_vehicle(Player player)
v3               get_player_coords(Player player)
number           get_player_health(Player player)
number           get_player_armour(Player player)
number           get_player_max_health(Player player)
number           get_player_heading(Player player)
Player           get_player_from_ped(Ped ped)
number           get_player_team(Player player)
Vehicle          get_player_vehicle(Player player)
boolean          is_player_vehicle_god(Player player)
boolean          is_player_host(Player player)
nill             get_host()
Hash             get_player_model(Player player)
nill             unset_player_as_modder(Player player)
boolean          is_player_valid(Player player)
number           get_player_host_token(Player player)
nill             set_player_targeting_mode(Player player, number targetMode)
```
 __Ped Functions__ 
```
boolean          is_ped_in_any_vehicle(Ped ped)
nill             set_group_formation(number groupId, number formationType)
nill             set_ped_as_group_member(Ped ped, number groupId)
number           get_ped_group(Ped ped)
nill             get_group_size(number groupID, Any *unknown, number *sizeInMembers)
number           get_ped_health(Ped ped)
nill             set_ped_health(Entity entity, null health, null p2 = 0)
boolean          is_ped_ragdoll(Ped ped)
boolean          is_ped_a_player(Ped ped)
Hash             get_current_ped_weapon(Ped)
nill             set_ped_nullo_vehicle(Ped ped, Vehicle vehicle, number seatIndex)
number           get_ped_drawable_variation(Ped ped, number componentId)
number           get_ped_prop_index(Ped ped, number componentId) 
number           get_ped_prop_texture_index(Ped ped, number componentId) 
boolean          set_ped_component_variation(Ped ped, number componentId, number drawableId, number textureId, number paletteId)   
boolean          set_ped_prop_index(Ped ped, number componentId, number drawableId, number textureId, booleanattach)
nill             set_ped_can_switch_weapons(Ped ped, boolean toggle)
boolean          is_ped_shooting(Ped ped)
number           get_ped_bone_index(Ped ped, number boneId)
Hash             get_ped_relationship_group_hash(Ped ped)      
nill             set_ped_relationship_group_hash(Ped ped, Hash hash)
Vehicle          get_vehicle_ped_is_using(Ped, ped, booleanlastVehicle)
nill             clear_all_ped_props(Ped ped)
number           clear_ped_tasks_immediately(Ped ped)
nill             clear_ped_blood_damage(Ped ped)
boolean          is_ped_in_vehicle(Ped ped, Vehicle vehicle)
boolean          is_ped_using_any_scenario(Ped ped)
boolean          set_ped_to_ragdoll(Ped ped, number time1, number time2, number type)
boolean          set_ped_can_ragdoll(Ped ped, boolean toggle)
boolean          can_ped_ragdoll(Ped ped)
boolean          set_ped_combat_ability(Ped ped, number ability)
number           get_ped_max_health(Ped ped)
boolean          set_ped_max_health(Ped ped, number health)
boolean          resurrect_ped(Ped ped)
nill             set_ped_combat_movement(Ped ped, number value)
nill             set_ped_combat_range(Ped ped, number value)
nill             set_ped_combat_attributes(Ped ped, number attributes)
nill             set_ped_accuracy(Ped ped, number accuracy)
Ped              create_ped(number type, Hash model, v3 pos, number heading, boolean isNetworked, boolean unk1)
null             get_number_of_ped_drawable_variations(Ped ped, number componentId)
null             get_number_of_ped_texture_variations(Ped ped, number componentId)
null             get_number_of_ped_prop_drawable_variations(Ped ped, number propId)
null             get_number_of_ped_prop_texture_variations(Ped ped, number propId)
nill             set_ped_random_component_variation(Ped ped, number unknown)
nill             set_ped_default_component_variation(Ped ped, number unknown)
nill             set_ped_movement_clipset(Ped ped, string clipSet, number unknownt)
nill             reset_ped_movement_clipset(Ped ped, number unknown)
Ped              clone_ped(Ped ped)
boolean          set_ped_config_flag(Ped ped, number flag, boolean value)
boolean          set_ped_ragdoll_blocking_flags(Ped ped, null flags)
boolean          reset_ped_ragdoll_blocking_flags(Ped ped, number flags)
nill             set_ped_density_multiplier_this_frame(number value)
nill             set_scenario_ped_density_multiplier_this_frame(number p0, number p1)
Ped              get_all_peds()
Group            create_group()
nill             remove_group(number group)
nill             set_ped_as_group_leader(Ped ped, number group)
nill             remove_ped_from_group(Ped ped)
boolean          is_ped_group_member(Ped ped, number group)
boolean          set_group_formation_spacing(number group, number p1, number p2, number p3)
boolean          reset_group_formation_default_spacing(number group)
nill             set_ped_never_leaves_group(Ped ped, boolean toggle)
boolean          does_group_exist(number group)
boolean          is_ped_in_group(Ped ped)
nill             set_create_random_cops(boolean toggle)
boolean          can_create_random_cops()
boolean          is_ped_swimming(Ped ped)
boolean          is_ped_swimming_underwater(Ped ped)
nill             clear_relationship_between_groups(number relationship, Hash firstGroup, Hash secondGroup)
nill             set_relationship_between_groups(number relationship, Hash firstGroup, Hash secondGroup)
boolean          set_ped_head_blend_data(Ped ped, number shapeFirstID, number shapeSecondID, number shapeThirdID, number skinFirstID, number skinSecondID, number skinThirdID, number shapeMix, number skinMix, number thirdMix, boolean isParent)
boolean          set_ped_hair_colors(Ped ped, number colorID, number highlightColorID)
boolean          set_ped_eye_color(Ped ped, number index)
boolean          set_ped_head_overlay_color(Ped ped, number overlayID, number colorType, number colorID, number secondColorID)
```
 __Entity Functions__ 
```
v3               get_entity_coords(Entity entity)
boolean          set_entity_coords_no_offset(Entity entity, number xPos, number yPos, number zPos, boolean xAxis, boolean yAxis, boolean zAxis)
v3               get_entity_rotation(Entity entity)
boolean          set_entity_rotation(Entity entity, number pitch, number roll, number yaw, number rotationOrder, boolean p5)
boolean          set_entity_heading(Entity entity, number heading)
boolean          set_entity_velocity(Entity entity, number x, number y, number z)
boolean          is_an_entity(number handle)
boolean          is_entity_a_ped(Entity entity)
boolean          is_entity_a_vehicle(Entity entity)
boolean          is_entity_an_object(Entity entity)
boolean          is_entity_dead(Entity entity)
boolean          is_entity_on_fire(Entity entity)
boolean          is_entity_visible(Entity entity)
boolean          is_entity_attached(Entity entity)
boolean          set_entity_visible(Entity entity, boolean toggle, boolean unk)
number           get_entity_type(Entity entity)
boolean          set_entity_gravity(Entity entity, boolean toggle)
nill             apply_force_to_entity(Entity entity, number forceFlags, number x, number y, number z, number offX, number offY, number offZ, number boneIndex, boolean isDirectionRel, boolean ignoreUpVec, boolean isForceRel, boolean p12, boolean p13)
Entity           get_entity_attached_to(Entity entity)
boolean          detach_entity(Entity entity, boolean p1, boolean collision)
Hash             get_entity_model_hash(Entity entity)
number           get_entity_heading(Entity entity)
boolean          attach_entity_to_entity(Entity subject, Entity target, number boneIndex, v3 offset, v3 rot, booleansoftPinning, booleancollision, booleanisPed, number vertexIndex, booleanfixedRot)
nill             set_entity_as_mission_entity(Entity entity, boolean p1, boolean p2)
boolean          set_entity_collision(Entity entity, boolean toggle, boolean keepPhysics)
boolean          is_entity_in_air(Entity entity)
boolean          set_entity_as_no_longer_needed(Entity entity)
boolean          set_entity_no_collsion_entity(Entity entity, Entity entity2, boolean thisFrameOnly)
nill             freeze_entity(Entity entity, boolean toggle)
boolean,v3       get_entity_offset_from_coords(Entity entity, number posX, number posY, number posZ)
nill             set_entity_alpha(Entity entity, number alphaLevel, boolean skin)
boolean          delete_entity(Entity entity)
nill             set_entity_god_mode(Entity entity, boolean toggle)
boolean          get_entity_god_mode(Entity entity)
boolean          is_entity_in_water(Entity entity)
number           get_entity_speed(Entity entity)
nill             set_entity_lights(Entity entity, boolean toggle)
nill             set_entity_max_speed(Entity entity, number speed)
number           get_entity_pitch(Entity entity)
number           get_entity_roll(Entity entity)
v3               get_entity_physics_rotation(Entity entity)
number           get_entity_physics_heading(Entity entity)
number           get_entity_physics_pitch(Entity entity)
number           get_entity_physics_roll(Entity entity)
boolean          does_entity_have_physics(Entity entity)
v3               get_entity_rotation_velocity(Entity entity)
number           get_entity_submerged_level(Entity entity)
number           get_entity_population_type(Entity entity)
boolean          is_entity_static(Entity entity)
boolean          is_entity_in_zone(Entity entity, string zone)
boolean          is_entity_upright(Entity entity, number angle)
boolean          is_entity_upside_down(Entity entity)
boolean          has_entity_been_damaged_by_any_object(Entity entity)
boolean          has_entity_been_damaged_by_any_vehicle(Entity entity)
boolean          has_entity_been_damaged_by_any_ped(Entity entity)
boolean          has_entity_been_damaged_by_entity(Entity entity1, Entity entity2)
boolean          does_entity_have_drawable(Entity entity)
boolean          has_entity_collided_with_anything(Entity entity)
number           get_entity_bone_index_by_name(Entity entity, string name)
```
 __Weapon Functions__ 
```
nill              give_delayed_weapon_to_ped(Ped ped, Hash weapon, number ammoCount, boolean equip)
number            get_weapon_tint_count(Ped ped, Hash weapon)
number            get_ped_weapon_tint_index(Ped ped, Hash weapon, number index)
nill              give_weapon_component_to_ped(Ped ped, Hash weapon, Hash componentHas)
nill              remove_all_ped_weaponsPed ped, boolean p1)
nill              remove_weapon_from_ped(Ped ped, Hash weapon)
boolean,number    get_max_ammo(Ped ped, Hash weapon)
boolean           set_ped_ammo(Ped ped, Hash weapon, number ammo)
nill              remove_weapon_component_from_ped(Ped ped, Hash weapon, Hash component)
boolean           has_ped_got_weapon_component(Ped ped, Hash weapon, Hash component)
Hash              get_ped_ammo_type_from_weapon(Ped ped, Hash weapon)
nill              set_ped_ammo_by_type(Ped ped, Hash type, number amount)
boolean           has_ped_got_weapon(Ped ped, Hash weapon)
Hash              get_all_weapon_hashes()
string            get_weapon_name(Hash weapon)
number            get_weapon_weapon_wheel_slot(Hash weapon)
Hash              get_weapon_model(Hash weapon)
Hash              get_weapon_audio_item(Hash weapon)
Hash              get_weapon_slot(Hash weapon)
number            get_weapon_ammo_type(Hash weapon)
Hash              get_weapon_weapon_group(Hash weapon)
Hash              get_weapon_weapon_type(Hash weapon)
Hash              get_weapon_pickup(Hash weapon)
```
 __Object Functions__ 
```
Object            create_object(Hash model, v3 pos, boolean networked, boolean dynamic)
Object            create_world_object(Hash model, v3 pos, boolean networked, boolean dynamic)
Object            get_all_objects()
Pickup            get_all_pickups()
```

 __Vehicle Functions__
```
nill              set_vehicle_tire_smoke_color(Vehicle vehicle, number r, number g, number b)
Ped               get_ped_in_vehicle_seat(Vehicle vehicle, number seat)
number            get_free_seat(Vehicle vehicle)
boolean           is_vehicle_full(Vehicle vehicle)
nill              set_vehicle_stolen(Vehicle vehicle, boolean value)
boolean           set_vehicle_color(Vehicle vehicle, number r, number g, number b)
string            get_mod_text_label(Vehicle vehicle, number modType, number modvalue)
string            get_mod_slot_name(Vehicle vehicle, number modType)
number            get_num_vehicle_mods(Vehicle vehicle, number modType)
boolean           set_vehicle_mod(Vehicle vehicle, number type, number modIndex, booleancustomTires)
number            get_vehicle_mod(Vehicle vehicle, number type)
boolean           set_vehicle_mod_kit_type(Vehicle vehicle, number kit)
nill              set_vehicle_extra(Vehicle vehicle, number extra)
boolean           does_extra_exist(Vehicle vehicle, number extra)
boolean           is_vehicle_extra_turned_on(Vehicle vehicle, number extra)
nill              toggle_vehicle_mod(Vehicle vehicle, number type, boolean toggle)
nill              set_vehicle_bulletproof_tires(Vehicle vehicle, boolean toggle)
boolean           is_vehicle_a_convertible(Vehicle vehicle)
boolean           get_convertible_roof_state(Vehicle vehicle)
nill              set_convertible_roof(Vehicle vehicle, boolean open)
nill              set_vehicle_indicator_lights(Vehicle vehicle, number turnSignal, boolean toggle)
nill              set_vehicle_brake_lights(Vehicle vehicle, boolean toggle)
nill              set_vehicle_can_be_visibly_damaged(Vehicle vehicle, boolean toggle)
nill              set_vehicle_engine_on(Vehicle vehicle, boolean toggle, boolean instantly, boolean noAutoTurnOn)
nill              set_vehicle_fixed(Vehicle vehicle)
nill              set_vehicle_deformation_fixed(Vehicle vehicle)
nill              set_vehicle_undriveable(Vehicle vehicle, boolean toggle)
boolean           set_vehicle_on_ground_properly(Vehicle vehicle, number p1)
nill              set_vehicle_forward_speed(Vehicle vehicle, number speed)
nill              set_vehicle_number_plate_text(Vehicle vehicle, string plateText)
nill              set_vehicle_door_open(Vehicle vehicle, number doorIndex, boolean loose, boolean openInstantly)
nill              set_vehicle_doors_shut(Vehicle vehicle, boolean closeInstantly)
boolean           is_toggle_mod_on(Vehicle vehicle, number type)
nill              set_vehicle_wheel_type(Vehicle vehicle, number wheelType)
nill              set_vehicle_number_plate_index(Vehicle vehicle, number plateIndex)
nill              set_vehicle_tires_can_burst(Vehicle vehicle, boolean toggle)
nill              set_vehicle_tire_burst(Vehicle vehicle, number index, boolean onRim, number p3)
number            get_num_vehicle_mod(Vehicle vehicle, number type)
boolean           is_vehicle_engine_running(Vehicle vehicle)
nill              set_vehicle_engine_health(Vehicle vehicle, number health)
boolean           is_vehicle_damaged(Vehicle vehicle)
boolean           is_vehicle_on_all_wheels(Vehicle vehicle)
Vehicle           create_vehicle(Hash model, v3 pos, number heading, boolean networked, boolean alwaysFalse)
boolean           set_vehicle_doors_locked(Vehicle vehicle, number lockStatus)
boolean           set_vehicle_neon_lights_color(Vehicle vehicle, number r, number g, number b)
number            get_vehicle_neon_lights_color(Vehicle vehicle)
boolean           set_vehicle_neon_light_enabled(Vehicle vehicle, number index, boolean toggle)
boolean           is_vehicle_neon_light_enabled(Vehicle vehicle, number index)
nill              set_vehicle_density_multipliers_this_frame(number multiplier)
nill              set_random_vehicle_density_multiplier_this_frame(number multiplier)
nill              set_parked_vehicle_density_multiplier_this_frame(number multiplier)
nill              set_ambient_vehicle_range_multiplier_this_frame(number multiplier)
boolean           is_vehicle_rocket_boost_active(Vehicle vehicle)
nill              set_vehicle_rocket_boost_active(Vehicle vehicle, boolean active)
nill              set_vehicle_rocket_boost_percentage(Vehicle vehicle, number percentage)
nill              control_landing_gear(Vehicle vehicle, number state)
number            get_landing_gear_state(Vehicle vehicle)
number            get_vehicle_livery(Vehicle vehicle)
boolean           set_vehicle_livery(Vehicle vehicle, number index)
boolean           is_vehicle_stopped(Vehicle vehicle)
number            get_vehicle_number_of_passengers(Vehicle vehicle)
number            get_vehicle_max_number_of_passengers(Vehicle vehicle)
number            get_vehicle_model_number_of_seats(Hash model)
number            get_vehicle_livery_count(Vehicle vehicle)
number            get_vehicle_roof_livery_count(Vehicle vehicle)
boolean           is_vehicle_model(Vehicle vehicle, Hash model)
boolean           is_vehicle_stuck_on_roof(Vehicle vehicle)
nill              set_vehicle_doors_locked_for_player(Vehicle vehicle, Player player, boolean toggle)
boolean           get_vehicle_doors_locked_for_player(Vehicle vehicle, Player player)
nill              set_vehicle_doors_locked_for_all_players(Vehicle vehicle, boolean toggle)
nill              set_vehicle_doors_locked_for_non_script_players(Vehicle vehicle, boolean toggle)
nill              set_vehicle_doors_locked_for_team(Vehicle vehicle, number team, boolean toggle)
nill              explode_vehicle(Vehicle vehicle, boolean audible, boolean invisible)
nill              set_vehicle_out_of_control(Vehicle vehicle, booleankillDriver, boolean explodeOnImpact)
nill              set_vehicle_timed_explosion(Vehicle vehicle, Ped ped, boolean toggle)
nill              add_vehicle_phone_explosive_device(Vehicle vehicle)
boolean           has_vehicle_phone_explosive_device()
nill              detonate_vehicle_phone_explosive_device()
nill              set_taxi_lights(Vehicle vehicle, boolean state)
boolean           is_taxi_light_on(Vehicle vehicle)
boolean           set_vehicle_colors(Vehicle vehicle, number colorPrimary, number colorSecondary)
boolean           set_vehicle_extra_colors(Vehicle vehicle, number pearlescentColor, number wheelColor)
number            get_vehicle_primary_color(Vehicle vehicle)
number            get_vehicle_secondary_color(Vehicle vehicle)
boolean           set_vehicle_fullbeam(Vehicle vehicle, boolean toggle)
string            get_livery_name(Vehicle vehicle, number index)
nill              set_vehicle_window_tint(Vehicle vehicle, number tint)
number            get_vehicle_window_tint(Vehicle vehicle, number tint)
Hash              get_all_vehicle_model_hashes()
Vehicle           get_all_vehicles()
nill              modify_vehicle_top_speed(Vehicle vehicle, number value)
nill              set_vehicle_engine_torque_multiplier_this_frame(Vehicle vehicle, number value)
nill              set_heli_blades_full_speed(Vehicle vehicle)
nill              set_heli_blades_speed(Vehicle vehicle, number speed)
nill              set_vehicle_parachute_active(Vehicle vehicle, boolean active)
boolean           does_vehicle_have_parachute(Vehicle vehicle)
boolean           can_vehicle_parachute_be_activated(Vehicle vehicle)
nill              set_vehicle_can_be_locked_on(Vehicle vehicle, boolean canBeLockedOn, boolean unknown)
boolean           set_vehicle_reduce_grip(Vehicle vehicle, boolean toggle)
number            get_vehicle_estimated_max_speed(Vehicle vehicle)
```

 __Streaming Functions__
```
boolean           request_model(Hash model)
boolean           has_model_loaded(Hash model)
boolean           set_model_as_no_longer_needed(Hash model)
boolean           is_model_in_cdimage(Hash model)
boolean           is_model_valueid(Hash model)
boolean           is_model_a_plane(Hash model)
boolean           is_model_a_vehicle(Hash model)
boolean           is_model_a_heli(Hash model)
nill              request_ipl(string iplName)
nill              remove_ipl(string iplName)
nill              request_anim_set(string animSet)
boolean           has_anim_set_loaded(string animSet)
nill              request_anim_dict(string animDict)
boolean           has_anim_dict_loaded(string animDict)
boolean           is_model_a_bike(Hash model)
boolean           is_model_a_car(Hash model)
boolean           is_model_a_bicycle(Hash model)
boolean           is_model_a_quad(Hash model)
boolean           is_model_a_boat(Hash model)
boolean           is_model_a_train(Hash model)
boolean           is_model_a_ped(Hash model)
nill              remove_anim_dict(string animDict)
nill              remove_anim_set(string animSet)
```

 __Gameplay Functions__
```
Hash             get_hash_key(string hash)
nill             display_onscreen_keyboard(number p0, string windowTitle, string p2, string defaultText, string defaultConcat1, string defaultConcat2, string defaultConcat3, number maxInputLength)
boolean          update_onscreen_keyboard()
string           get_onscreen_keyboard_result()
nill             set_override_weather(string weather)
nill             clear_override_weather()
nill             set_blackout(boolean state)
nill             set_mobile_radio(boolean state)
nill             clear_area_of_objects(number x, number y, number z, number radius, number flags)
nill             clear_area_of_vehicles(number x, number y, number z, number radius, number flags)
nill             clear_area_of_peds(number x, number y, number z, number radius, number flags)
nill             clear_area_of_cops(number x, number y, number z, number radius, number flags)
number           get_cloud_hat_opacity()
nill             preload_cloud_hat(string szName)
nill             clear_cloud_hat()
nill             load_cloud_hat(string name, number transitionTime)
nill             unload_cloud_hat(string szName, number a2)
boolean,number   get_ground_z(number x, number y, number z, number *groundZ, boolean unk, boolean p)
number           get_frame_count()
number           get_frame_time()
boolean          shoot_single_bullet_between_coords(number x1, number y1, number z1, number x2, number y2, number z2, number damage, bool p7, Hash weaponHash, Ped ownerPed, boolean isAudible, boolean isInvisible, number speed, Entity entity, Any p14)
```   

 __Fire Functions__
```
boolean          add_explosion(number x, number y, number z, number explosionType, number damageScale, bool isAudible, boolean isInvisible, number cameraShake boolean noDamage)
Ped              start_entity_fire(Entity entity)
nill             stop_entity_fire(Entity entity)
```

 __Network Functions__
```
boolean           network_is_host()
boolean           has_control_of_entity(Entity entity)
boolean           request_control_of_entity(Entity entity)
boolean           is_session_started()
nill              network_session_kick_player(Player player)
boolean           is_friend_online(string name)
boolean           is_friend_in_multiplayer(string name)
number            get_friend_scid(string name)
number            get_friend_count()
number            get_max_friends()
Hash              network_hash_from_player(Player player)
boolean           is_friend_index_online(number index)
boolean           send_chat_message(string message, boolean team)
```
 __Cutscene Functions__

```
nill              stop_cutscene_immediately()
nill              remove_cutscene()
boolean           is_cutscene_active()
boolean           is_cutscene_playing()
```
 __Control Functions__
```
boolean           disable_control_action(number padIndex, number control, boolean disable)
boolean           is_control_just_pressed(number padIndex, number control)
boolean           is_disabled_control_just_pressed(number padIndex, number control)
boolean           is_control_pressed(number padIndex, number control)
boolean           is_disabled_control_pressed(number padIndex, number control)
number            get_control_normal(number padIndex, number control)
boolean           set_control_normal(number padIndex, number control, number value)
```   

 __Graphics Functions__

```
number            get_screen_height()
number            get_screen_width()
nill              request_named_ptfx_asset(string fxName)
boolean           has_named_ptfx_asset_loaded(string fxName)
nill              remove_named_ptfx_asset(string fxName)
nill              set_next_ptfx_asset(string fxName)
nill              set_next_ptfx_asset_by_hash(Hash fxName)
```

 __Time Functions__
```
nill              set_clock_time(number hour, number minute, number second)
number            get_clock_hours()
number            get_clock_minutes()
number            get_clock_seconds()
```

 __Decorator Functions__ 
```
nill              decor_register(string propertyName, number type)
boolean           decor_exists_on(Entity entity, string propertyName)
boolean           decor_remove(Entity entity, string propertyName)
number            decor_get_number(Entity entity, string propertyName)
boolean           decor_set_number(Entity entity, string propertyName, number value)
number            decor_get_number(Entity entity, string propertyName)
boolean           decor_set_number(Entity entity, string propertyName, number value)
boolean           decor_get_boolean(Entity entity, string propertyName)
boolean           decor_set_boolean(Entity entity, string propertyName, boolean value)
boolean           decor_set_time(Entity entity, string name, number timeStamp)
```
 __Interior Functions__
```
Any               get_numbererior_from_entity(Entity entity)
Any               get_numbererior_at_coords_with_type(number x, number y, number z, string numbereriorType)
nill              disable_numbererior_prop(Interior interior, boolean toggle)
nill              refresh_numbererior(Interior interior)
```
 __Water Functions__
```
number            get_waves_numberensity()
nill              set_waves_numberensity(number numberensity)
nill              reset_waves_numberensity()
```
 __Stat Functions__
```
number            stat_get_number(Hash hash, number unk0)
number            stat_get_number(Hash hash, number unk0)
boolean           stat_get_boolean(Hash hash, number unk0)
boolean           stat_set_number(Hash hash, number value, boolean save)
boolean           stat_set_number(Hash hash, number value, boolean save)
boolean           stat_set_boolean(Hash hash, booleanvalue, boolean save)
```

 __Cam Functions__
```
v3                get_gameplay_cam_rot()
v3                get_gameplay_cam_pos()
number            get_gameplay_cam_relative_pitch()
number            get_gameplay_cam_relative_yaw()
```

 __UI Functions__
```
 Entity           get_entity_from_blip(Entity entity)
 Blip             get_blip_from_entity(Entity entity)
 Blip             add_blip_for_entity(Entity entity)
 boolean          set_blip_sprite(Blip blip, number spriteId)
 boolean          set_blip_colour(Blip blip, number colour)
 nill             hide_hud_component_this_frame(number id)
 nill             hide_hud_and_radar_this_frame()
 string           get_label_text(string labelName)
 nill             draw_rect(v2 position, v2 size, Color color)
 nill             draw_line(number x1, number y1, number z1, number x2, number y2, flonumberat z2, number red, number green, number blue, number alpha)
 nill             draw_text(string text, number font, v2 position, number size, Color color, boolean centered, boolean rightjustified, boolean outlined)
 nill             set_text_scale(number scale, number size)
 nill             set_text_color(number red, number green, number blue, number alpha)
 nill             set_text_font(number font)
 nill             set_text_wrap(number start, number end)
 nill             set_text_outline()
 nill             set_text_centre(boolean allign)
 nill             set_text_right_justify(boolean toggle)
 nill             set_text_justification(number justifyType)
 nill             set_new_wayponumber(number x, number y)
 v2               get_wayponumber_coord()
 boolean          is_hud_component_active(number id)
 nill             show_hud_component_this_frame(number id)
 nill             set_wayponumber_off()
 boolean          set_blip_as_mission_creator_blip(Blip blip, boolean toggle)
 boolean          is_mission_creator_blip(Blip blip)
 Blip             add_blip_for_radius(number x, number y, number z,  number radius)
 Blip             add_blip_for_pickup(Pickup pickup)
 Blip             add_blip_for_coord(v3 pos)
 nill             set_blip_coord(Blip blip, number x, number y, number z)
 v3               get_blip_coord(Blip blip)
 boolean          remove_blip(Blip blip)
 nill             set_blip_route(Blip blip, boolean toggle)
 nill             set_blip_route_color(Blip blip, number color)
```  

 __Sound Functions__
```
nill              play_sound(number soundId, string audioName, string audioRef, boolean p3, Any p4, boolean p5)
nill              play_sound_frontend(number soundId, string audioName, string audioRef, boolean p4)
nill              play_sound_from_entity(number soundId, string audioName, Entity entity, string audioRef)
nill              play_sound_from_coord(number soundId, string audioName, number x, number y, number z, string audioRef, boolean isNetwork, number range, boolean p8)
nill              stop_sound(number soundId)
```
 __Ai Fuctions__ 
```
nill              task_goto_entity(Entity entity, Entity target, number duration, number distance, number speed)
boolean           ask_combat_ped(Ped ped, Ped targetPed, number a1, number a2)
Any               task_go_to_coord_by_any_means(Ped ped, number x, number y, number z, number speed, Any p5, boolean p6, number walkingStyle, number p8)
boolean           task_wander_standard(Ped ped, number p1, number p2)
nill              task_vehicle_drive_wander(Ped ped, Vehicle vehicle, number speed, number driveStyle)
nill              task_start_scenario_in_place(Ped ped, string name, number unkDelay, boolean playEnterAnim)
nill              task_start_scenario_at_position(Ped ped, string scenarioName, number x, number y, number z, number heading, number duration, boolean sittingScenario, boolean teleport)
nill              task_stand_guard(Ped ped, number x, number y, number z, number heading, string scenarioNamee)
nill              play_anim_on_running_scenario(Ped ped, string animDict, string animName)
boolean           does_scenario_group_exist(string scenarioGroup)
boolean           is_scenario_group_enabled(string scenarioGroup)
boolean           set_scenario_group_enabled(string scenarioGroup)
nill              reset_scenario_groups_enabled()
boolean           set_exclusive_scenario_group(string scenarioGroup)
boolean           reset_exclusive_scenario_group()
boolean           is_scenario_type_enabled(string scenarioType, boolean enabled)
boolean           set_scenario_type_enabled(string scenarioName, boolean p1)
nill              reset_scenario_types_enabled()
boolean           is_ped_active_in_scenario(Ped ped)
nill              task_follow_to_offset_of_entity(Ped ped, Entity entity, number offsetX, number offsetY, number offsetZ, number movementSpeed, number timeout, number stoppingRange, boolean persistFollowing)
nill              task_vehicle_drive_to_coord_longrange(Ped ped, Vehicle vehicle, number x, number y, number z, number speed, number driveMode, number stopRange)
nill              task_shoot_at_entity(Entity entity, Entity target, number duration, Hash firingPattern)
nill              task_vehicle_escort(Ped ped, Vehicle vehicle, Vehicle targetVehicle, number mode, number speed, number drivingStyle, number minDistance, number a8, number noRoadsDistance)
nill              task_vehicle_follow(Ped driver, Vehicle vehicle, Entity targetEntity, number speed, number drivingStyle, number minDistance)
nill              task_vehicle_drive_to_coord(Ped ped, Vehicle vehicle, number x, number y, number z, number speed, Any p6, Hash vehicleModel, number drivingMode, number stopRange, number p10)
nill              task_vehicle_shoot_at_coord(Ped ped, number x, number y, number z, number p4)
nill              task_vehicle_shoot_at_ped(Ped ped, Ped target, number p2)
nill              task_vehicle_aim_at_coord(Ped ped, number x, number y, number z)
nill              task_vehicle_aim_at_ped(Ped ped, Ped target)
nill              task_stay_in_cover(Ped ped)
nill              task_go_to_coord_while_aiming_at_coord(Ped ped, number x, number y, number z, number aimAtX, number aimAtY, number aimAtZ, number moveSpeed, boolean p8, number p9, number p10, bool p11, Any flags, boolean p13, Hash firingPattern)
nill              task_go_to_coord_while_aiming_at_entity(Any p0, number p1, number p2, number p3, Any p4, number p5, boolean p6, number p7, number p8, boolean p9, Any p10, boolean p11, Any p12, Any p13)
nill              task_go_to_entity_while_aming_at_coord(Any p0, Any p1, number p2, number p3, number p4, number p5, boolean p6, number p7, number p8, boolean p9, bool p10, Any p11)
nill              task_go_to_entity_while_aiming_at_entity(Ped ped, Entity entityToWalkTo, Entity entityToAimAt, number speed, boolean shootatEntity, number p5, number p6, boolean p7, boolean p8, Hash firingPattern)
nill              task_open_vehicle_door(Ped ped, Vehicle vehicle, number timeOut, number doorIndex, number speed)
nill              task_enter_vehicle(Ped ped, Vehicle vehicle, number timeout, number seat, number speed, number flag, Any p6)
nill              task_leave_vehicle(Ped ped, Vehicle vehicle, number timeout, number seat, number speed, number flag, Any p6)
nill              task_sky_dive(Ped ped, boolean p1)
nill              task_parachute(Ped ped, boolean p1, boolean p2)
nill              task_parachute_to_target(Ped ped, number x, number y, number z)
nill              set_parachute_task_target(Ped ped, number x, number y, number z)
nill              set_parachute_task_thrust(Ped ped, number thrust)
nill              task_rappel_from_heli(Ped ped, number p1)
nill              task_vehicle_chase(Ped driver, Entity targetEnt)
nill              set_task_vehicle_chase_behaviour_flag(Ped ped, number flag, boolean set)
nill              set_task_vehicle_chase_ideal_persuit_distance(Ped ped, number distance)
nill              task_shoot_gun_at_coord(Ped ped, number x, number y, number z, number duration, Hash firingPattern)
nill              task_aim_gun_at_coord(Ped ped, number x, number y, number z, int time, boolean p5, boolean p6)
nill              task_turn_ped_to_face_entity(Ped ped, Entity entity, number duration)
nill              task_aim_gun_at_entity(Ped ped, Entity entity, number duration, boolean p3)
boolean           is_task_active(Ped ped, number taskIndex)
boolean           task_play_anim(Ped ped, string animDictionary, string animationName, number speed, number speedMultiplier, number duration, number flag, number playbackRate, boolean lockX, boolean lockY, boolean lockZ)
nill              stop_anim_task(Ped ped, string animDictionary, string animationName, number p3)
```

 __Script Functions__
```
nill              trigger_script_event(number eventId, Player player, number[] params)
```

 __System Functions__
```
nill              yield(number nanoSeconds)
nill              wait(number nanoSeconds)
```